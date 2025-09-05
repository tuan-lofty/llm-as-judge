# Numerical Metric Prompt

## Metric Configuration
- **Type**: Numerical
- **Range**: {min_value} to {max_value} (integers)
- **Description**: {metric_description}

## Rails
You must output ONLY a valid JSON object with the following structure:

```json
{
  "metric_data_type": "numerical",
  "evaluation_result": {
    "score": "integer"
  },
  "reasoning": "string"
}
```

### Output Rules:
- Output must be valid JSON only
- No additional text, explanations, or markdown formatting outside the JSON
- score must be an integer within the range {min_value} to {max_value} (inclusive)
- reasoning must be a non-empty string explaining your evaluation decision
- metric_data_type must be exactly "numerical"
- score CANNOT be outside the specified range - if evaluation would result in out-of-range value, use the closest valid boundary value

### Examples:
- Range: 1-10, Result: 7 → Output: `{"metric_data_type": "numerical", "evaluation_result": {"score": 7}, "reasoning": "The response covers most of the expected information with minor formatting differences."}`
- Range: 0-100, Result: 85 → Output: `{"metric_data_type": "numerical", "evaluation_result": {"score": 85}, "reasoning": "The output is highly accurate and complete, exceeding expectations."}`
- Range: -5 to 5, Result: 3 → Output: `{"metric_data_type": "numerical", "evaluation_result": {"score": 3}, "reasoning": "The response is partially correct but missing key information."}`

### Invalid Examples:
- Range: 1-10, Result: 7 → Output: `7` ❌
- Range: 1-10, Result: 7 → Output: `{"score": 7}` ❌
- Range: 1-10, Result: 7 → Output: `{"metric_data_type": "numerical", "score": 7}` ❌
- Range: 1-10, Result: 15 → Output: `{"metric_data_type": "numerical", "evaluation_result": {"score": 15}, "reasoning": "..."}` ❌ (score out of range)
- Range: 1-10, Result: 0 → Output: `{"metric_data_type": "numerical", "evaluation_result": {"score": 0}, "reasoning": "..."}` ❌ (score out of range)

Remember: Output ONLY the complete JSON object, nothing else.
