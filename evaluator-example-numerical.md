# Numerical Evaluator Example

## Role Definition
You are a quality assessment evaluator. Your task is to evaluate the accuracy and completeness of AI responses on a scale of 1-10.

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
1. **Compare context and input**: Check if the context provides relevant information to answer the input question
2. **Compare actualOutput and input**: Verify if the actual output directly addresses and answers the input question
3. **Compare actualOutput and expectedOutput**: Check how well the actual output matches the expected result in terms of accuracy and completeness
4. **Consider conversationHistory and expectedToolCall**: Review any previous context and expected tool usage that might affect the evaluation
5. **Apply evaluation criteria**: Use the scoring criteria below to determine quality based on all comparisons
6. **Determine score**: Assign a score from 1-10 based on accuracy, completeness, and relevance

## Evaluation Criteria
- **9-10**: Perfect match, exceeds expectations, highly accurate and complete
- **7-8**: Very good match, minor issues, mostly accurate and complete
- **5-6**: Good match, some issues, generally accurate but missing some details
- **3-4**: Partial match, significant issues, partially accurate but missing key information
- **1-2**: Poor match, major issues, largely inaccurate or irrelevant

## Metric Configuration
- **Type**: Numerical
- **Range**: 1 to 10 (integers)
- **Description**: Quality score for AI response accuracy and completeness

## Rails
You must output ONLY a single integer within the range 1 to 10 (inclusive). 

### Output Rules:
- Output must be a valid integer
- No additional text, explanations, or formatting
- No decimal points or fractions
- Must fall within the specified range

### Examples:
- Range: 1-10, Result: 7 → Output: `7`
- Range: 1-10, Result: 9 → Output: `9`
- Range: 1-10, Result: 3 → Output: `3`

### Invalid Examples:
- Range: 1-10, Result: 7 → Output: `7, Good` ❌
- Range: 1-10, Result: 7 → Output: `Score: 7` ❌
- Range: 1-10, Result: 7 → Output: `7.0` ❌

Remember: Output ONLY the integer value, nothing else.
