# MultiTransform - Step-Based Data Transformation Engine

## Overview

The `multiTransform` module provides a powerful, step-based transformation engine that allows complex data processing through a sequence of configurable operations. It supports conditional logic, string operations, and asynchronous processing with a pipeline approach.

## Location

```
src/functions/utilities/multiTransform.ts
```

## Dependencies

- `valuesSingleton.ts` - Global values and configuration
- `console_log.ts` - Logging functionality

## Type Definitions

### TMultiTransformArgs<T>

```typescript
type TMultiTransformArgs<T> = {
  args: { [key: string]: any };
  steps: TSteps<T>[];
  result?: T;
}
```

Main configuration object for transformation operations.

#### Properties

- `args: { [key: string]: any }` - Dynamic arguments available to all steps
- `steps: TSteps<T>[]` - Array of transformation steps to execute
- `result?: T` - Optional result storage

### TSteps<T>

```typescript
type TSteps<T> = {
  argument2Use: string;
  condition?: (args: { [key: string]: any }) => boolean;
  jumpTo?: number;
} & (
  | { type: 'replace' }
  | { type: 'replaceAll' }
  | { type: 'divide' }
  | { type: 'return'; callBack: (args: unknown) => T }
)
```

Individual transformation step configuration with conditional logic and operation types.

#### Common Properties

- `argument2Use: string` - Key reference for arguments (supports separator-delimited multi-args)
- `condition?: function` - Optional condition to determine step execution
- `jumpTo?: number` - Optional step index to jump to when condition fails

#### Operation Types

- **replace**: Single string replacement operation
- **replaceAll**: Global string replacement with regex
- **divide**: Direct value assignment
- **return**: Callback-based transformation with result

## Core Function

### multiTransform<T>()

```typescript
async multiTransform<T>(args: TMultiTransformArgs<T>): Promise<T>
```

Executes a sequence of transformation steps with conditional logic and error handling.

#### Parameters

- `args: TMultiTransformArgs<T>` - Configuration object with arguments and steps

#### Returns

- `Promise<T>` - Transformed result of specified type

#### Processing Pipeline

1. **Step Iteration**: Loops through steps array with index tracking
2. **Condition Evaluation**: Checks optional conditions before step execution
3. **Jump Logic**: Handles conditional jumps to different step indices
4. **Operation Dispatch**: Executes operation based on step type
5. **Result Management**: Tracks and returns final transformation result

## Operation Types

### Replace Operation

```typescript
type: 'replace'
```

Performs single string replacement using three arguments from `argument2Use`.

#### Argument Structure

```
argument2Use: "source{separator}searchValue{separator}replaceValue"
```

#### Processing

1. Splits `argument2Use` by values separator
2. Gets source string from args[0]
3. Replaces first occurrence of args[1] with args[2]
4. Stores result in `args.lastReplace`

### ReplaceAll Operation

```typescript
type: 'replaceAll'
```

Performs global string replacement using regex pattern.

#### Processing

1. Creates RegExp from second argument with global flag
2. Replaces all occurrences in source string
3. Stores result in `args.lastReplace`

### Divide Operation

```typescript
type: 'divide'
```

Direct value assignment to result.

#### Processing

1. Gets value from specified argument
2. Assigns directly to `args.result`

### Return Operation

```typescript
type: 'return'
callBack: (args: unknown) => T
```

Callback-based transformation with custom logic.

#### Processing

1. Calls provided callback with specified argument
2. Awaits result if callback is async
3. Assigns result to `args.result`

## Usage Examples

### Basic String Transformation

```typescript
const transformConfig = {
  args: {
    sourceText: "Hello World",
    searchTerm: "World",
    replacement: "Universe"
  },
  steps: [
    {
      argument2Use: "sourceText{separator}searchTerm{separator}replacement",
      type: 'replace' as const
    }
  ]
};

const result = await multiTransform(transformConfig);
// Result: "Hello Universe" (stored in args.lastReplace)
```

### Conditional Processing

```typescript
const conditionalConfig = {
  args: {
    value: "test-string",
    shouldProcess: true
  },
  steps: [
    {
      argument2Use: "value",
      condition: (args) => args.shouldProcess,
      jumpTo: 2,
      type: 'replace' as const
    },
    {
      argument2Use: "value",
      type: 'divide' as const
    }
  ]
};
```

### Callback Processing

```typescript
const callbackConfig = {
  args: {
    inputData: "raw-data"
  },
  steps: [
    {
      argument2Use: "inputData",
      type: 'return' as const,
      callBack: async (data) => {
        // Custom transformation logic
        return processData(data);
      }
    }
  ]
};
```

## Error Handling

### Try-Catch Structure

- Wraps entire processing in try-catch block
- Logs errors using `console_log.consoleLog()`
- Throws standardized error messages

### Result Validation

- Checks for result existence before return
- Throws "No result" error if result is undefined
- Ensures type safety through generic constraints

## Architecture Integration

### Value System Integration

- Uses `ValuesSingleton` for separator configuration
- Accesses global values through singleton pattern
- Maintains consistency with library-wide standards

### Asynchronous Processing

- Supports async conditions and callbacks
- Maintains promise chain throughout pipeline
- Handles mixed sync/async operations

## Performance Considerations

### Step Execution

- Sequential processing with controlled flow
- Efficient condition evaluation with short-circuiting
- Minimal memory allocation during transformation

### Error Recovery

- Graceful degradation on processing errors
- Comprehensive error logging for debugging
- Fail-fast approach with meaningful error messages

## Integration Points

- Used in complex CSS value transformations
- Applied in configuration processing pipelines
- Integrated with string manipulation utilities
- Utilized in conditional CSS generation logic
