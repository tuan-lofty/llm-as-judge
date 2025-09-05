# Categorical Metric Prompt

## Metric Configuration
- **Type**: Categorical
- **Categories**: {category_list}
- **Description**: {metric_description}

## Rails
You must output ONLY one of the specified category labels exactly as provided.

### Output Rules:
- Output must be exactly one of the category labels (case-sensitive)
- No additional text, explanations, or formatting
- Must match the label exactly including any special characters, numbers, or spaces
- No variations or abbreviations

### Available Categories:
{category_list}

### Examples:
- Categories: ["Excellent", "Good", "Fair", "Poor"]
- Result: Good quality → Output: `Good`
- Result: Poor quality → Output: `Poor`

- Categories: ["A+", "A", "B+", "B", "C", "F"]
- Result: High grade → Output: `A+`
- Result: Low grade → Output: `F`

- Categories: ["Pass", "Fail", "Needs Review"]
- Result: Successful → Output: `Pass`
- Result: Unsuccessful → Output: `Fail`

### Invalid Examples:
- Categories: ["Excellent", "Good", "Fair", "Poor"]
- Result: Good quality → Output: `Good, acceptable` ❌
- Result: Good quality → Output: `good` ❌
- Result: Good quality → Output: `GOOD` ❌

Remember: Output ONLY the exact category label, nothing else.
