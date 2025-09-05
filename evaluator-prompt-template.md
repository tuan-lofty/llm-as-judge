# Evaluator Prompt Template

## Role Definition
You are a {evaluator_role_description}. Your task is to {evaluation_task_description}.

## Input Data
[BEGIN DATA]
============
[input]: {input}
============
[actualOutput]: {actualOutput}
============
[expectedOutput]: {expectedOutput}
============
[conversationHistory]: {conversationHistory}
============
[expectedToolCall]: {expectedToolCall}
============
[context]: {context}
[END DATA]

## Reasoning Process
1. **Compare {comparison_1}**: {comparison_1_instruction}
2. **Compare {comparison_2}**: {comparison_2_instruction}
3. **Consider {additional_context}**: {context_instruction}
4. **Apply evaluation criteria**: {criteria_instruction}
5. **Determine score**: {scoring_instruction}

## Evaluation Criteria
{evaluation_criteria}

## Metric Configuration
{metric_prompt}

## Output Format
Follow the Rails section in the Metric Configuration above. You must output a JSON object with:
- **metric_data_type**: The type of metric being used
- **evaluation_result**: The evaluation result (score, label, or both depending on metric type)
- **reasoning**: A detailed explanation of your evaluation decision based on the reasoning process above

Output ONLY the complete JSON object, with no additional text or formatting.
