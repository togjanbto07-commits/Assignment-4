# Assignment-4
LangChain project

Teacher Efficiency Agent
LangGraph + Gemini AI Pipeline
This notebook builds a 4-node LangGraph pipeline that:

1. Ingests a teacher working-hours Excel file
2. Calls Gemini LLM to evaluate each teacher's monthly efficiency (Pydantic structured output)
3. Calls Gemini LLM again to write an executive summary per month (Pydantic structured output)
4. Exports a fully formatted, color-coded Excel report


The LLM receives these computed metrics per teacher per month:

Completion Rate = (Actual Hours / Scheduled Hours) × 100% — the core metric
Replacements Given — how many times the teacher gave away their class (absence indicator)
Replacements Received — how many times they covered for others (extra workload)
Sessions with Notes/Issues — count of flagged sessions

The LLM then weighs all of these together to output an Efficiency Score from 0–100, guided by this logic in the prompt:
High score (80-100) → high completion rate + low replacements given + few notes
Medium score (60-79) → some missed sessions or notes present
Low score (0-59)    → low completion rate + multiple absences/replacements given


Efficiency Score = (Completion Rate × 0.5)
                 + (Reliability Score × 0.3)
                 + (Stability Score × 0.2)

Where:
  Completion Rate   = (Actual Hours / Scheduled Hours) × 100

  Reliability Score = max(0, 100 - (Replacements_Given × 20))
                      — lose 20 pts per class given away

  Stability Score   = max(0, 100 - (Sessions_with_Notes × 10))
                      — lose 10 pts per flagged session
Weights rationale:

50% on hours completion — did they show up and teach?
30% on reliability — did they need to be replaced?
20% on stability — were there issues/incidents?
