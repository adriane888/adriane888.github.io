---
layout: post
title: "GitHub Actions Composite Input Issue"
date: 2025-10-05 00:00:00 +0000
categories: actions github
---

## A Limitation With GitHub Actions Composite Input
I like to use GitHub Action Workflows and Composites and if you are smart about it, they can be crazy useful at saving time and energy. Let me start by giving a high level definition

### Shared Workflow
A shared workflow is a whole reusable workflow. Think end to end of any given task. That being build, test and deploying all in one shared bundle that can be used across multiple environments without the need to copy and paste the workflow. And if any changes need to be made, they can all be done in one location

### Composite Actions
Composite Actions are more granular. They are reusable steps that would be located within a workflow. You can also use them within your shared workflow, giving even more reusability. Need a set of shell commands ran but need it done in multiple locations? Use Composite actions. 

### The Limitation

Composites have no dynamic matrix generation for action inputs. This means all outputs are strings. This is an issue because, let's say you have a complicated shell script that is dynamic in nature. You use true/false (boolean) as logic gates to run sections of the script. Now you can see the issue: you can't use dynamic matrix generation for action inputs, so now you can't use those inputs as booleans, right? Kinda. 

### Using fromJSON To Interpret Boolean-Like Inputs

Even though composite action inputs are always strings, you can still treat certain values like booleans inside workflow-level conditionals by wrapping them with the built-in `fromJSON()` expression function. This is handy when you pass inputs such as `"true"`, `"false"`, or even a JSON array/object string and want to branch logic.

#### Example: Reusable (Shared) Workflow Consuming a Boolean String

```yaml
# .github/workflows/build.yml (called via workflow_call)
on:
	workflow_call:
		inputs:
			greenhills:
				description: "Whether to build using GreenHills toolchain"
				required: false
				default: "false" # strings only
			builder_access_token:
				required: true
				type: string

jobs:
	build:
		runs-on: ubuntu-latest
		steps:
			- name: Debug greenhills input
				if: runner.os == 'Linux'
				run: |
					echo "greenhills raw='${{ inputs.greenhills }}'"
					echo "greenhills parsed='${{ fromJSON(inputs.greenhills) }}'"

			- name: Resolve x64 Build Dependencies
				# Run only when NOT building GreenHills
				if: runner.os == 'Linux' && fromJSON(inputs.greenhills) == false
				env:
					BUILDER_ACCESS_TOKEN: ${{ inputs.builder_access_token }}
				run: python ci_utilities/dependencies.py

			- name: Resolve GreenHills Build Dependencies
				if: runner.os == 'Linux' && fromJSON(inputs.greenhills) == true
				env:
					BUILDER_ACCESS_TOKEN: ${{ inputs.builder_access_token }}
				run: python ci_utilities/dependencies.py --ghx
```

In the example above, `inputs.greenhills` is a string, but `fromJSON(inputs.greenhills)` converts the JSON literal `"true"` or `"false"` into an actual boolean for the conditional expression.

#### Example: Composite Action Accepting a Boolean-Like Input

```yaml
# .github/actions/setup/action.yml
name: "Setup"
description: "Example composite action using fromJSON on an input"
inputs:
	enable-feature:
		description: "Enable the experimental feature"
		required: false
		default: "false"
runs:
	using: composite
	steps:
		- name: Always echo raw value
			shell: bash
			run: echo "enable-feature raw='${{ inputs.enable-feature }}'"

		- name: Conditionally run feature block
			if: fromJSON(inputs.enable-feature) == true
			shell: bash
			run: |
				echo "Experimental feature enabled"
				./enable_feature.sh
```

Because composite steps cannot themselves declare outputs as booleans or use matrices, this pattern lets you still branch logic based on user-provided strings representing JSON literals.

#### Tips for Reliable Parsing

1. Only use exact lowercase `"true"` / `"false"` or valid JSON (e.g. `"[\"a\",\"b\"]"`) when you expect `fromJSON` to succeed.
2. Guard against empty values: `if: inputs.flag != '' && fromJSON(inputs.flag) == true`.
3. For multi-value inputs, pass a JSON array string and iterate by using `fromJSON(inputs.items)` in a matrix (only possible at workflow level, not inside a composite).
4. Avoid accidental spaces: `" true"` will throw an evaluation error because it's not valid JSON.

This approach sidesteps the limitation: while inputs remain strings, you regain logical branching by interpreting those strings as structured JSON.