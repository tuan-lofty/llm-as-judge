# Boolean Metric Prompt

## Metric Configuration
- **Type**: Boolean
- **Values**: {true_label} / {false_label}
- **Description**: {metric_description}

## Rails
You must output ONLY a valid JSON object with the following structure:

```json
{
  "metric_data_type": "boolean",
  "evaluation_result": {
    "score": "boolean"
  },
  "reasoning": "string"
}
```

### Output Rules:
- Output must be valid JSON only
- No additional text, explanations, or markdown formatting outside the JSON
- score must be exactly `true` or `false` (lowercase, unquoted)
- reasoning must be a non-empty string explaining your evaluation decision
- metric_data_type must be exactly "boolean"
- score CANNOT be any other value - only `true` or `false` are valid

### Examples:
- Result: Positive → Output: `{"metric_data_type": "boolean", "evaluation_result": {"score": true}, "reasoning": "The response is correct and matches the expected output."}`
- Result: Negative → Output: `{"metric_data_type": "boolean", "evaluation_result": {"score": false}, "reasoning": "The response is incorrect and does not match the expected output."}`
- Result: Correct → Output: `{"metric_data_type": "boolean", "evaluation_result": {"score": true}, "reasoning": "The actual output accurately addresses the input question."}`
- Result: Incorrect → Output: `{"metric_data_type": "boolean", "evaluation_result": {"score": false}, "reasoning": "The actual output contains errors or is irrelevant to the input."}`

### Invalid Examples:
- Result: Positive → Output: `true` ❌
- Result: Positive → Output: `{"score": true}` ❌
- Result: Positive → Output: `{"metric_data_type": "boolean", "score": true}` ❌
- Result: Positive → Output: `{"metric_data_type": "boolean", "evaluation_result": {"score": "yes"}, "reasoning": "..."}` ❌ (invalid boolean value)
- Result: Positive → Output: `{"metric_data_type": "boolean", "evaluation_result": {"score": 1}, "reasoning": "..."}` ❌ (invalid boolean value)
- Result: Positive → Output: `{"metric_data_type": "boolean", "evaluation_result": {"score": "True"}, "reasoning": "..."}` ❌ (invalid boolean value)

Remember: Output ONLY the complete JSON object, nothing else.
