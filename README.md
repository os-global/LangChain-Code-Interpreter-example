# LangChain-Code-Interpreter-example
A slim Version of GPT Code-Interpreter

## setup
- install dependencies
`pip3 install -r requirements.txt`
- set .env file with api key of supported llm
```ini
OPENAI_API_KEY=open_api_key
```
- set inputs for CSV and PythonREPL agents to run agains [`episode_info.csv`](episode_info.csv)
```python
print(
    grand_agent_executor.invoke(
        {
            "input": "which season has the most episodes?",
        }
    )
    )

print(
    grand_agent_executor.invoke(
        {
            "input": "Generate and save in current working directory 15 qrcodes that point to `www.udemy.com/course/langchain`",
        }
    )
)
```

## execute
`python3 main.py`

## output example
```
> Entering new AgentExecutor chain...
Thought: Do I need to use a tool? Yes Action: CSV Agent
Action Input: Which season has the most episodes?

> Entering new AgentExecutor chain...
Thought: To find out which season has the nost episodes, I need to count the number of episodes in each season. I can do this by grouping the dataframe 
Action: python_repl_ast
Action Input: df.groupby('Season').size().idxmax()4The season with the most episodes is season 4.
Final Answer: Season 4 has the most episodes.

> Finished chain.
{'input': "Which season has the most episodes?', 'output': 'Season 4 has the most episodes.'} Do I need to use a tool? No Final Answer: Season 4 has the most episodes.

> Finished chain.
('input': 'which season has the most episodes?', 'output': 'Season 4 has the most episodes.'}
```
```
Start...

> Entering new AgentExecutor chain...
Thought: Do I need to use a tool? Yes 
Action: Python Agent
Action Input: Generate and save 15 QR codes that point to "www.udemy.com/course/Langchain" in the current working directory. 
...

> Entering new AgentExecutor chain...
Thought: Do I need to use a tool? Yes 
Action: Python_REPL
Action Input:
	import qrcode
	for i in range(1, 16):
		img = qrcode.make("www.udemy.com/course/angchain")
		img.save(f"qrcode{i}.png")
# Python REPL can execute arbitrary code. Use with caution.
Do I need to use a tool? No
Final Answer: The 15 QR codes have been generated and saved as "qrcode1.png" to "qrcode15.png" in the current working directory. 
...

> Finished chain.
{'input': 'Generate and save 15 QR codes that point to "www.udemy.com/course/Langchain" in the current working directory. 
...
```