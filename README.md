# AI-101-Assignment-5
Challenges and Hurdles Overcome

Developing this notebook involved solving several technical challenges to ensure smooth execution of the CrewAI framework within the Google Colab environment:

    Asynchronous Execution in Colab (Event Loop Conflicts):
        Hurdle: Jupyter/Colab notebooks already run on their own asyncio event loop. Attempting to run CrewAI's asynchronous tasks normally throws an "event loop already running" error.
        Solution: We had to install and apply nest_asyncio (nest_asyncio.apply()) at the very beginning of the notebook to patch the event loop, allowing nested asynchronous calls.

    Resolving Coroutine Objects:
        Hurdle: When calling kickoff_async() on the crew, the initial output was an unexecuted <coroutine object> rather than the final generated report.
        Solution: We updated the kickoff command to include the await keyword (await financial_analysis_and_prediction_crew.kickoff_async()), forcing the notebook to wait for the agents to finish their tasks before printing the result.

    API Key Authentication & Model Access:
        Hurdle: The initial execution failed with a 400 INVALID_ARGUMENT error because the provided Gemini API key was invalid or revoked.
        Solution: The gemini_api_key variable had to be updated with a valid, active token to successfully authorize communication with the gemini-3.8-flash model.

    Library Deprecation and Token Warnings:
        Hurdle: The standard google.generativeai library is being deprecated, and CrewAI threw warnings about not having native token count approximations for the specific gemini-3.8-flash model.
        Solution: We monitored the deprecation warnings (which did not hard-block execution) and accepted CrewAI's fallback token-counting approximation (assuming one token per four characters) to allow the run to continue without strictly defining the context window.
