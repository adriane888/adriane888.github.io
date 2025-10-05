---
layout: post
title: "Copilot Spaces"
date: 2025-10-05 00:00:00 +0000
categories: copilot github ai
---

Copilot Spaces
Copilot spaces is the newest iteration of tooling brought to us by GitHub. It became generally available Sep 24th. I am getting whiplash from all of these new/replacement tools being introduced. But I am pretty happy with this inclusion. 

I came across the future while looking into Copilot knowledge bases. I was notified of its retirement, being replaced by, you guessed it, Spaces. Knowledge bases felt clunky at the best of times, and it was a pain to get set up and work. Spaces seem quite a bit more strait forward and have better utility IMO. 

Let’s kick things off with how to set it up, then we can go deeper. 
1.	Navigate to https://github.com/copilot/spaces or when in GitHub, click on the copilot icon face in the top right corner then navigate to spaces on the left panel
2.	Click create space and give it a name
3.	Select who you would like the owner to be. If you would like to share the space with others from your organization, select that organization
4.	Click create space
5.	Then, I would highly suggest creating a description. But this does not effect responses
Next, let’s talk about the meat and potatoes, different contexts. We can add to this space, since in AI world, context is king.
•	Instructions: You can define copilot’s role up to 4000 characters. I suggest lining up the description of this space with the instructions you give it, especially if you are planning on sharing this space. Be concise
•	Files and Repos: Spaces will use the latest code on the main branch of your repository. For best result, specify the best files and folder for your spaces purpose for the best results
•	Link files, pull requests, and issues: This unfortunately is only for github content right now. Paist any URLs of GitHub content, including PRs and issues. (Would like to see the ability to search URLs for content on confluence or jira tickets) 
•	Upload file or Add text content: strait forward, you can add images text files, documents, and spreadsheets. Also text content. 
Now, how do we use the damn thing?
You got two options
1.	Use it right in the GitHub Copilot Spaces GUI. Select your space and start typing
2.	The more interesting way is via your IDE
From your IDE, you not only have added context of the file you need help coding on, but also the space you just set up. I find this works best in two situations. 
One, where there is a lack of documentation. The ability to help new or Jr devs by setting up a space where you curated Markdown files, examples, and other files and folders that best represent and explain your repo. Not to mention to automate the creation of those lacking documents. 
Two, distributed systems. Most modern solutions utilize distributed systems. That usually means distributed repos. Working from repo to repo and keeping the context strait can be a struggle. I find that having a companion AI agent that has the same context between multiple repos as you can save time. Create a space per system repo, and find yourself saving loads of time. 
Now how do you use it in your IDE? 
Your IDE needs to support two tools. GitHub Copilot extension, and GitHub MCP server. I use VS code. 
•	Link to install GitHub MCP Server: https://github.com/mcp/github/github-mcp-server
•	install GitHub Copilot extension in the extensions tab in VS Code
To use the GitHub MCP server and Spaces, in the chat box:
1.	Use this command “list_copilot_spaces”. This will list out the Spaces available. 
2.	Then, lead your prompt with “get_copilot_space” and the name of the space.
Now you should be all set to speed up your workflow with Spaces! It is not a perfect tool, but used right, it can definitely help you and your team acheave you goals quicker, and if nothing else, have some AI fun. 
