# JSON Output Structure for Frontend Integration

## Overview
All evaluator prompts now output a standardized JSON object with three main fields:
- `metric_data_type`: Identifies the type of metric being used
- `evaluation_result`: Contains the actual evaluation result (varies by metric type)
- `reasoning`: Provides detailed justification for the evaluation decision

## JSON Structure by Metric Type

### 1. Numerical Metric
```json
{
  "metric_data_type": "numerical",
  "evaluation_result": {
    "score": "integer"
  },
  "reasoning": "string"
}
```

**Example:**
```json
{
  "metric_data_type": "numerical",
  "evaluation_result": {
    "score": 7
  },
  "reasoning": "The response covers most of the expected information with minor formatting differences."
}
```

### 2. Boolean Metric
```json
{
  "metric_data_type": "boolean",
  "evaluation_result": {
    "score": "boolean"
  },
  "reasoning": "string"
}
```

**Example:**
```json
{
  "metric_data_type": "boolean",
  "evaluation_result": {
    "score": true
  },
  "reasoning": "The response is correct and matches the expected output."
}
```

### 3. Categorical Metric
```json
{
  "metric_data_type": "categorical",
  "evaluation_result": {
    "label": "string"
  },
  "reasoning": "string"
}
```

**Example:**
```json
{
  "metric_data_type": "categorical",
  "evaluation_result": {
    "label": "Good"
  },
  "reasoning": "The response is mostly accurate with minor issues that don't significantly impact quality."
}
```

### 4. Range Quality Metric
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

**Example:**
```json
{
  "metric_data_type": "range_quality",
  "evaluation_result": {
    "score": 7,
    "label": "Good"
  },
  "reasoning": "The response is mostly accurate with minor issues that don't significantly impact quality."
}
```

## Frontend Integration Guidelines

### Metric Output Column
The `evaluation_result` field should be rendered based on the `metric_data_type`:

- **numerical**: Display the `score` value
- **boolean**: Display the `score` value (true/false)
- **categorical**: Display the `label` value
- **range_quality**: Display both `score` and `label` values

### Reasoning Column
The `reasoning` field should be displayed as-is to provide insight into the evaluator's justification.

### Data Type Validation
Always check the `metric_data_type` field to ensure proper rendering:
- Validate that the expected fields exist in `evaluation_result`
- Validate that values are within the specified ranges/options
- Handle missing or malformed JSON gracefully
- Provide fallback display for unexpected data types

### Value Validation by Type
- **Numerical**: Ensure score is within the specified min-max range
- **Boolean**: Ensure score is exactly `true` or `false`
- **Categorical**: Ensure label exactly matches one of the provided categories (case-sensitive)
- **Range Quality**: Ensure score is within range AND label matches the range mapping for that score

### Error Handling
If the JSON is malformed or missing required fields:
- Display an error message in the Metric Output column
- Show "No reasoning available" in the Reasoning column
- Log the error for debugging purposes

If values are outside the specified ranges/options:
- Display "Invalid value" in the Metric Output column
- Show the reasoning but add a warning about invalid values
- Log the validation error for debugging purposes

## Benefits for Frontend Development

1. **Consistent Structure**: All metrics follow the same JSON structure
2. **Type Safety**: `metric_data_type` field enables proper type checking
3. **Flexible Rendering**: Different metric types can be rendered appropriately
4. **Rich Context**: `reasoning` field provides valuable insights for users
5. **Easy Parsing**: Standardized JSON format simplifies frontend integration

## Example Frontend Implementation

```javascript
function renderEvaluationResult(evaluationData) {
  const { metric_data_type, evaluation_result, reasoning } = evaluationData;
  
  switch (metric_data_type) {
    case 'numerical':
      return {
        metricOutput: evaluation_result.score,
        reasoning: reasoning
      };
    case 'boolean':
      return {
        metricOutput: evaluation_result.score ? 'Correct' : 'Incorrect',
        reasoning: reasoning
      };
    case 'categorical':
      return {
        metricOutput: evaluation_result.label,
        reasoning: reasoning
      };
    case 'range_quality':
      return {
        metricOutput: `${evaluation_result.score} (${evaluation_result.label})`,
        reasoning: reasoning
      };
    default:
      return {
        metricOutput: 'Unknown metric type',
        reasoning: 'No reasoning available'
      };
  }
}
```
