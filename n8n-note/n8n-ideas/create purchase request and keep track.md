create a n8n workflow to create a purchase request

take a picture of the website + the url then send to the chat bot

the chat bot will use API token (any model that fit for this job, gpt, gemini, claude, etc)

chat bot will create a pr request based on the PR template, fill out the form based on the picture and the url, then use pandadoc api to create a a e-sign document to get approval

the pr will be save in google workspace, gg sheet for keep track

prerequisite:
- n8n host (local host on existing server)
- LLM api key: gpt, gemini, claude, or a local ollama using qwen with 4b or ollama cloud with free tier?  (need approval)
- google workspace (existing plan)
- pandadoc (need to check if current plan has API support, if not, switch to DocuSeal)
- DocuSeal (Self hosted, use oracle free tier to host, but required company payment to create an account)
