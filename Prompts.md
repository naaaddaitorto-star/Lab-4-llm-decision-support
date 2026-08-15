The Summary Prompt
1. This first summary prompt is less precise, and the output it gives is less formal.
print("\n--- SUMMARY_PROMPT_V1 Outputs ---")
SUMMARY_PROMPT_V1 = f" Summarize:."
2. For this summary, a role has been given to the model and system. The prompt also specifies the type of text to be summarized, and the context is detected as formal, so it produces a formal summary.
SUMMARY_PROMPT_V2_SYSTEM = "You are an assistant to a microfinance loan officer. Summarize loan applications factually, neutrally, with no invented details, in 3-4 sentences."
def SUMMARY_PROMPT_V2_USER(letter_text):
  return f"Summarize this loan application:\n\n{letter_text}."



The Extract Prompt
- For the extract prompt, what the system should recognize has been stated along with an example, with a sample letter and format for data to be extracted. Additionally, a limitation is set to prevent the model from hallucinating.

EXTRACT_PROMPT = """
Given the following information about a loan application, do the following:
- Extract the applicant's name as a string (key is applicant_name).
- Extract the amount the person is requesting for (key is amount_ghs).
- Extract the purpose of the loan (key is purpose).
- Extract the monthly profit the person is expecting (key is monthly_profit_ghs).
- Determine if the applicant has collateral or a guarantor as a boolean (key is has_collateral_or_guarantor).
- Extract the number of months the person is expecting to repay the loan (key is repayment_months).

Return this data strictly as a JSON object with no preamble or postamble. As a guide, here is a sample application, and the expected output:
Letter: "Dear Loan Manager, I am Anokor Tetteh, an apprentice at Dark and Lovely Beauty Salon, a student of Abrantie College. I request GHS 10,000 to purchase a kiosk to start my own salon and employ an apprentice. Last year, I earned a revenue of GHS 13,000; monthly profit averages GHS 1,500, and 
I hold a GHS 2,500 fixed deposit with Republic Bank, which I can pledge. Proposed repayment: GHS 500 monthly for 12 months. Unfortunately, I have no collateral at the moment, but God willing, everything will be fine."
Output:
{
    "applicant_name": "Anokor Tetteh",
    "amount_ghs": 10000,
    "purpose": "purchase a kiosk to start my own salon and employ an apprentice",
    "monthly_profit_ghs": 1500,
    "has_collateral_or_guarantor": false,
    "repayment_months": 12
}

Critical Information:
- The example provided is an example to guide you in the output format, not the example to run it on.
- If a field is not stated in the letter, use null. Do not guess. Return "null".
- Do not invent any details.

See the letter below:
"""




The Brief Prompt
This prompt also specifies how the model can categorize data and clarify its representation after extraction, which is then used to suggest the way forward in decision-making.

BRIEF_PROMPT = """
After receiving letters and extracting information from the JSON, add the following to produce a reccomendation breif do the following:
- List the strengths of each letter using bullet points to make reading clearer.
- Highlight risks in each letter and give clear output using bullet points.
- For missing data, if the output is null, none, or false, then it falls under the missing data category.
- Then suggest the next steps from the data given. The next step could be to: 
    - call the individual for an interview
    - Request an important document for confirmation 
    - flag for senior review.
NOTE: The final decision is made by the human senior officer and not the model.
"""
