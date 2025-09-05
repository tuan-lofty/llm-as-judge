# Range Quality Metric Prompt

## Metric Configuration
- **Type**: Range Quality
- **Range**: {min_value} to {max_value} (integers)
- **Quality Mappings**: {range_mappings}
- **Description**: {metric_description}

## Rails
You must output ONLY a valid JSON object with the following structure:

```json
{
  "metric_data_type": "range_quality",
  "evaluation_result": {
    "score": "integer",
    "label": "string"
  },
  "reasoning": "string"
}
```

### Output Rules:
- Output must be valid JSON only
- No additional text, explanations, or markdown formatting outside the JSON
- score must be an integer within the range {min_value} to {max_value} (inclusive)
- label must be the corresponding quality label from the range mappings
- reasoning must be a non-empty string explaining your evaluation decision
- metric_data_type must be exactly "range_quality"
- score and label MUST be consistent - the label must match the range mapping for the given score
- score CANNOT be outside the specified range
- label CANNOT be any value not defined in the range mappings

### Range Mappings:
{range_mappings}

### Examples:
- Range: 1-10, Mappings: [1-3: "Poor", 4-6: "Fair", 7-8: "Good", 9-10: "Excellent"]
- Result: Good quality → Output: `{"metric_data_type": "range_quality", "evaluation_result": {"score": 7, "label": "Good"}, "reasoning": "The response is mostly accurate with minor issues that don't significantly impact quality."}`
- Result: Excellent quality → Output: `{"metric_data_type": "range_quality", "evaluation_result": {"score": 9, "label": "Excellent"}, "reasoning": "The response exceeds expectations with exceptional accuracy and completeness."}`
- Result: Poor quality → Output: `{"metric_data_type": "range_quality", "evaluation_result": {"score": 2, "label": "Poor"}, "reasoning": "The response has significant issues and missing key information."}`

- Range: 0-100, Mappings: [0-30: "Low", 31-70: "Medium", 71-100: "High"]
- Result: Medium quality → Output: `{"metric_data_type": "range_quality", "evaluation_result": {"score": 50, "label": "Medium"}, "reasoning": "The response meets basic requirements but lacks some detail and precision."}`
- Result: High quality → Output: `{"metric_data_type": "range_quality", "evaluation_result": {"score": 85, "label": "High"}, "reasoning": "The response is highly accurate and complete with excellent detail."}`
- Result: Low quality → Output: `{"metric_data_type": "range_quality", "evaluation_result": {"score": 15, "label": "Low"}, "reasoning": "The response is largely incorrect or irrelevant to the input question."}`

### Invalid Examples:
- Range: 1-10, Result: Good quality → Output: `7` ❌
- Range: 1-10, Result: Good quality → Output: `{"score": 7, "label": "Good"}` ❌
- Range: 1-10, Result: Good quality → Output: `{"metric_data_type": "range_quality", "score": 7, "label": "Good"}` ❌
- Range: 1-10, Result: Good quality → Output: `{"metric_data_type": "range_quality", "evaluation_result": {"score": 15, "label": "Good"}, "reasoning": "..."}` ❌ (score out of range)
- Range: 1-10, Result: Good quality → Output: `{"metric_data_type": "range_quality", "evaluation_result": {"score": 7, "label": "Excellent"}, "reasoning": "..."}` ❌ (score-label mismatch)
- Range: 1-10, Result: Good quality → Output: `{"metric_data_type": "range_quality", "evaluation_result": {"score": 7, "label": "Average"}, "reasoning": "..."}` ❌ (label not in range mappings)

Remember: Output ONLY the complete JSON object, nothing else.
