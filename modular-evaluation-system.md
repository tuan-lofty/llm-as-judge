# Modular Evaluation System

## Overview
This system separates evaluation into two modular components:
1. **Metrics**: Define what values to output (score ranges, labels, etc.)
2. **Evaluator Prompts**: Define what to evaluate and how to reason about it

## System Architecture

### Metrics (Define What Value)
Metrics define the output format and constraints:
- **Numerical**: Integer ranges (e.g., 1-10, 0-100)
- **Boolean**: True/False values
- **Categorical**: Text labels (e.g., ["Excellent", "Good", "Fair", "Poor"])
- **Range Quality**: Integer ranges with quality mappings (e.g., 1-10 with [1-3: "Poor", 4-6: "Fair", 7-10: "Good"])

### Evaluator Prompts (Define What Target and How to Evaluate)
Evaluator prompts define:
- **Role**: What the evaluator does
- **Reasoning Process**: Specific comparisons to make (e.g., compare context and input to check retrieval quality, compare actualOutput and input to check response relevance)
- **Evaluation Logic**: How to evaluate the comparisons according to the metrics

## File Structure

### Metric Prompts
- `metric-numerical-prompt.md` - Integer range outputs
- `metric-boolean-prompt.md` - True/False outputs
- `metric-categorical-prompt.md` - Text label outputs
- `metric-range-quality-prompt.md` - Integer ranges with quality mappings

### Evaluator Templates
- `evaluator-prompt-template.md` - General template for creating evaluators
- `evaluator-example-numerical.md` - Example using numerical metric
- `evaluator-example-boolean.md` - Example using boolean metric
- `evaluator-example-categorical.md` - Example using categorical metric
- `evaluator-example-range-quality.md` - Example using range quality metric

## Usage Instructions

### Step 1: Choose a Metric Type
Select the appropriate metric based on your evaluation needs:
- **Numerical**: When you need a simple integer score
- **Boolean**: When you need a binary decision (correct/incorrect)
- **Categorical**: When you need predefined quality labels
- **Range Quality**: When you need detailed scoring with quality ranges

### Step 2: Configure the Metric
Customize the metric with your specific values:
- **Numerical**: Set min_value and max_value
- **Boolean**: Set true_label and false_label
- **Categorical**: Define your category list
- **Range Quality**: Set range and quality mappings

### Step 3: Create an Evaluator Prompt
Use the evaluator template and customize:
- **Role Definition**: Describe what the evaluator does
- **Reasoning Process**: Define specific comparisons to make (e.g., compare context and input to check retrieval quality, compare actualOutput and input to check response relevance)
- **Evaluation Criteria**: Define your scoring logic based on the comparisons
- **Metric Configuration**: Include your chosen metric

### Step 4: Combine Metric and Evaluator
The evaluator prompt should include the metric configuration in its "Metric Configuration" section.

## Example Combinations

### Numerical + Quality Assessment
- **Metric**: Numerical (1-10 range)
- **Evaluator**: Quality assessment evaluator comparing actualOutput vs expectedOutput
- **Result**: Integer score from 1-10

### Boolean + Correctness Check
- **Metric**: Boolean (true/false)
- **Evaluator**: Correctness evaluator comparing actualOutput vs expectedOutput
- **Result**: true or false

### Categorical + Quality Classification
- **Metric**: Categorical (["Excellent", "Good", "Fair", "Poor"])
- **Evaluator**: Quality classification evaluator comparing actualOutput vs expectedOutput
- **Result**: One of the category labels

### Range Quality + Comprehensive Evaluation
- **Metric**: Range Quality (1-10 with quality mappings)
- **Evaluator**: Comprehensive quality evaluator comparing actualOutput vs expectedOutput
- **Result**: Integer score from 1-10 (mapped to quality labels)

## Benefits of Modular Design

1. **Flexibility**: Mix and match different metrics with different evaluators
2. **Reusability**: Use the same metric with different evaluators
3. **Consistency**: Standardized output formats across different evaluation types
4. **Maintainability**: Update metrics or evaluators independently
5. **Clarity**: Clear separation between "what to output" and "what to evaluate"

## Customization Guidelines

### For Metrics:
- Keep Rails sections strict and focused on output format
- Provide clear examples of valid and invalid outputs
- Ensure all possible values are covered

### For Evaluator Prompts:
- Make role definitions specific to the evaluation task
- Clearly define specific comparisons to make in the reasoning process
- Provide detailed reasoning processes that connect comparisons to the metric
- Include comprehensive evaluation criteria based on the comparisons
