# Range Quality Metric Prompt

## Metric Configuration
- **Type**: Range Quality
- **Range**: {min_value} to {max_value} (integers)
- **Quality Mappings**: {range_mappings}
- **Description**: {metric_description}

## Rails
You must output ONLY a single integer within the range {min_value} to {max_value} (inclusive).

### Output Rules:
- Output must be a valid integer within the specified range
- No additional text, explanations, or formatting
- No decimal points or fractions
- Must fall within the specified range
- The integer will be mapped to its corresponding quality label based on the range mappings

### Range Mappings:
{range_mappings}

### Examples:
- Range: 1-10, Mappings: [1-3: "Poor", 4-6: "Fair", 7-8: "Good", 9-10: "Excellent"]
- Result: Good quality → Output: `7`
- Result: Excellent quality → Output: `9`
- Result: Poor quality → Output: `2`

- Range: 0-100, Mappings: [0-30: "Low", 31-70: "Medium", 71-100: "High"]
- Result: Medium quality → Output: `50`
- Result: High quality → Output: `85`
- Result: Low quality → Output: `15`

### Invalid Examples:
- Range: 1-10, Result: Good quality → Output: `7, Good` ❌
- Range: 1-10, Result: Good quality → Output: `Score: 7` ❌
- Range: 1-10, Result: Good quality → Output: `7.0` ❌
- Range: 1-10, Result: Good quality → Output: `Good` ❌

Remember: Output ONLY the integer value, nothing else. The quality label is determined by the range mappings.
