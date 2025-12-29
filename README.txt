MULTI-AGENT CONTENT MARKETING SYSTEM

PROJECT OVERVIEW

I built this project to create an intelligent multi-agent system for content marketing workflows. The system uses LangGraph and LangChain to coordinate multiple specialized AI agents that work together to research topics, create blog content, and generate social media posts.

The system consists of a content marketing manager that orchestrates three specialized worker agents: an online researcher, a blog manager, and a social media manager. Each agent has specific responsibilities and can communicate with the others through a shared state graph.

KEY FEATURES

Multi-Agent Architecture: The system uses LangGraph to create a stateful workflow where agents can pass information to each other and coordinate their work.

Content Marketing Manager: Acts as the orchestrator, deciding which agent should work next based on the current state of the project. It uses structured output to make routing decisions.

Online Researcher Agent: Specialized in finding and gathering information from the internet. It can process web content and extract relevant information for content creation.

Blog Manager Agent: Takes research findings and transforms them into polished, SEO-optimized blog articles. It focuses on content enhancement, SEO optimization, and editorial quality.

Social Media Manager Agent: Converts blog content into engaging social media posts, particularly optimized for Twitter. It condenses information while maintaining impact and engagement.

Web Content Processing Tool: A custom tool that fetches and processes content from URLs, with built-in error handling and URL validation.

TECHNOLOGY STACK

Python 3.13
LangChain 1.2.0 - For building LLM applications and agents
LangGraph 1.0.5 - For creating multi-agent workflows
LangChain Classic 1.0.1 - For agent execution and tool management
LangChain OpenAI 1.1.6 - For GPT-4 integration
BeautifulSoup4 - For web scraping and HTML parsing
Pydantic - For data validation and structured outputs
Python-dotenv - For environment variable management


HOW IT WORKS

The system operates as a state graph where each agent is a node. The content marketing manager acts as a router, deciding which agent should work next based on the current state and user requirements.

When you provide a task, the manager analyzes it and routes to the appropriate agent:
- Research tasks go to the online researcher
- Content creation tasks go to the blog manager  
- Social media tasks go to the social media manager
- When all tasks are complete, the manager signals FINISH

Each agent can use the process_search_tool to fetch and process web content from URLs. The tool includes validation to ensure URLs are properly formatted and handles errors gracefully.

The agents communicate through a shared state that contains messages and routing information. This allows them to build upon each other's work and maintain context throughout the workflow.

USAGE EXAMPLE

After setting up the environment and running all the notebook cells, you can use the system like this:

1. Compile the workflow by running the cell that creates the multiagent object.

2. Stream a task to the system. For example:

   for s in multiagent.stream(
       {
           "messages": [
               HumanMessage(
                   content="Write me a report on Agentic Behavior. After the research, pass the findings to the blog manager to generate the final blog article. Once done, pass it to the social media manager to write a tweet."
               )
           ],
       },
       {"recursion_limit": 150}
   ):
       if not "__end__" in s:
           print(s, end="\n\n-----------------\n\n")

The system will automatically route the task through the appropriate agents, with the manager coordinating the workflow.

PROJECT STRUCTURE

agents.ipynb - The main Jupyter notebook containing all the code
api.env - Environment variables file for API keys (not included in repository)
README.txt - This file

The notebook is organized into logical sections:
- Dependencies and imports
- Tool definitions
- Agent creation functions
- Individual agent setup
- Workflow graph construction
- Execution examples



I plan to add several enhancements in the future:

- Integration with web search APIs for better research capabilities
- Support for multiple content formats beyond blogs and tweets
- Enhanced error recovery and retry mechanisms
- Analytics and logging for agent performance
- Support for custom agent roles and workflows
- Integration with content management systems

CONTACT AND SUPPORT

This is a personal project I built to explore multi-agent systems and content automation. 