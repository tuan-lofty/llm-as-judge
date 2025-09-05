# Categorical Metric Prompt

## Metric Configuration
- **Type**: Categorical
- **Categories**: {category_list}
- **Description**: {metric_description}

## Rails
You must output ONLY a valid JSON object with the following structure:

```json
{
  "metric_data_type": "categorical",
  "evaluation_result": {
    "label": "string"
  },
  "reasoning": "string"
}
```

### Output Rules:
- Output must be valid JSON only
- No additional text, explanations, or markdown formatting outside the JSON
- label must be exactly one of the category labels (case-sensitive)
- reasoning must be a non-empty string explaining your evaluation decision
- metric_data_type must be exactly "categorical"
- Must match the label exactly including any special characters, numbers, or spaces
- label CANNOT be any value not in the provided category list

### Available Categories:
{category_list}

### Examples:
- Categories: ["Excellent", "Good", "Fair", "Poor"]
- Result: Good quality → Output: `{"metric_data_type": "categorical", "evaluation_result": {"label": "Good"}, "reasoning": "The response is mostly accurate with minor issues that don't significantly impact quality."}`
- Result: Poor quality → Output: `{"metric_data_type": "categorical", "evaluation_result": {"label": "Poor"}, "reasoning": "The response has significant issues and missing key information."}`

- Categories: ["A+", "A", "B+", "B", "C", "F"]
- Result: High grade → Output: `{"metric_data_type": "categorical", "evaluation_result": {"label": "A+"}, "reasoning": "The response exceeds expectations with exceptional accuracy and completeness."}`
- Result: Low grade → Output: `{"metric_data_type": "categorical", "evaluation_result": {"label": "F"}, "reasoning": "The response is largely incorrect or irrelevant to the input question."}`

- Categories: ["Pass", "Fail", "Needs Review"]
- Result: Successful → Output: `{"metric_data_type": "categorical", "evaluation_result": {"label": "Pass"}, "reasoning": "The response meets the required criteria and addresses the input appropriately."}`
- Result: Unsuccessful → Output: `{"metric_data_type": "categorical", "evaluation_result": {"label": "Fail"}, "reasoning": "The response does not meet the required criteria or contains significant errors."}`

### Invalid Examples:
- Categories: ["Excellent", "Good", "Fair", "Poor"]
- Result: Good quality → Output: `Good` ❌
- Result: Good quality → Output: `{"label": "Good"}` ❌
- Result: Good quality → Output: `{"metric_data_type": "categorical", "label": "Good"}` ❌
- Result: Good quality → Output: `{"metric_data_type": "categorical", "evaluation_result": {"label": "Average"}, "reasoning": "..."}` ❌ (label not in category list)
- Result: Good quality → Output: `{"metric_data_type": "categorical", "evaluation_result": {"label": "good"}, "reasoning": "..."}` ❌ (case-sensitive mismatch)
- Result: Good quality → Output: `{"metric_data_type": "categorical", "evaluation_result": {"label": "Very Good"}, "reasoning": "..."}` ❌ (label not in category list)

Remember: Output ONLY the complete JSON object, nothing else.
