# Assignment-4
LangChain project

Teacher Efficiency Agent
LangGraph + Gemini AI Pipeline
This notebook builds a 4-node LangGraph pipeline that:

1. Ingests a teacher working-hours Excel file
2. Calls Gemini LLM to evaluate each teacher's monthly efficiency (Pydantic structured output)
3. Calls Gemini LLM again to write an executive summary per month (Pydantic structured output)
4. Exports a fully formatted, color-coded Excel report
