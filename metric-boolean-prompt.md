# Boolean Metric Prompt

## Metric Configuration
- **Type**: Boolean
- **Values**: {true_label} / {false_label}
- **Description**: {metric_description}

## Rails
You must output ONLY one of the two boolean values: `true` or `false`.

### Output Rules:
- Output must be exactly `true` or `false` (lowercase, unquoted)
- No additional text, explanations, or formatting
- No variations like "True", "TRUE", "yes", "no", "1", "0"
- Must be a valid boolean value

### Examples:
- Result: Positive → Output: `true`
- Result: Negative → Output: `false`
- Result: Correct → Output: `true`
- Result: Incorrect → Output: `false`

### Invalid Examples:
- Result: Positive → Output: `true, correct` ❌
- Result: Positive → Output: `True` ❌
- Result: Positive → Output: `yes` ❌
- Result: Positive → Output: `1` ❌

Remember: Output ONLY `true` or `false`, nothing else.
