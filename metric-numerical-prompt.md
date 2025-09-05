# Numerical Metric Prompt

## Metric Configuration
- **Type**: Numerical
- **Range**: {min_value} to {max_value} (integers)
- **Description**: {metric_description}

## Rails
You must output ONLY a single integer within the range {min_value} to {max_value} (inclusive). 

### Output Rules:
- Output must be a valid integer
- No additional text, explanations, or formatting
- No decimal points or fractions
- Must fall within the specified range

### Examples:
- Range: 1-10, Result: 7 → Output: `7`
- Range: 0-100, Result: 85 → Output: `85`
- Range: -5 to 5, Result: 3 → Output: `3`

### Invalid Examples:
- Range: 1-10, Result: 7 → Output: `7, Good` ❌
- Range: 1-10, Result: 7 → Output: `Score: 7` ❌
- Range: 1-10, Result: 7 → Output: `7.0` ❌

Remember: Output ONLY the integer value, nothing else.
