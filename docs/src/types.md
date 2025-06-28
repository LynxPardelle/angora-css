# types.ts

## Overview

This file defines core TypeScript types used throughout the Angora CSS library. It establishes the type system foundation for the entire project.

## Purpose

- Defines fundamental types for the library
- Provides type safety for various operations
- Establishes contracts for data structures

## Types Defined

### TLOG_TYPE

```typescript
export type TLOG_TYPE = TObjectValues<typeof LOG_TYPES>
```

**Purpose:** Defines valid console log types (log, info, trace, error).

**Values:** "log" | "info" | "trace" | "error"

### TBPS

```typescript
export type TBPS = {
  bp: string;
  value: string;
  class2Create?: string;
};
```

**Purpose:** Defines the structure for breakpoint objects.

**Properties:**
- `bp`: Breakpoint identifier
- `value`: CSS value for the breakpoint
- `class2Create`: Optional CSS class to create

### TConsoleParser

```typescript
export type TConsoleParser = {
  type?: TLOG_TYPE;
  thing: any;
  style?: string;
  line?: string | null;
  stoper?: boolean;
};
```

**Purpose:** Defines configuration for console parsing operations.

**Properties:**
- `type`: Optional log type (defaults to "log")
- `thing`: The content to log
- `style`: Optional styling for console output
- `line`: Optional line information
- `stoper`: Optional flag to stop execution

### TPseudo

```typescript
export type TPseudo = {
  mask: string;
  real: string;
};
```

**Purpose:** Defines pseudo-element/pseudo-class mapping structure.

**Properties:**
- `mask`: The abbreviated or masked representation
- `real`: The actual CSS pseudo-element/class

### TAbreviationTraductor

```typescript
export type TAbreviationTraductor = {
  abreviation: string;
  abreviationRegExp: RegExp;
  traduction: string;
  traductionRegExp: RegExp;
};
```

**Purpose:** Defines abbreviation translation rules.

**Properties:**
- `abreviation`: The abbreviated form
- `abreviationRegExp`: Regular expression for matching abbreviations
- `traduction`: The full translation
- `traductionRegExp`: Regular expression for matching translations

## Constants

### LOG_TYPES

```typescript
const LOG_TYPES = {
  log: "log",
  info: "info",
  trace: "trace",
  error: "error",
} as const;
```

**Purpose:** Defines available console log types as a constant object.

## Utility Types

### TObjectValues<T>

```typescript
type TObjectValues<T> = T[keyof T];
```

**Purpose:** Utility type to extract values from an object type.

## Dependencies

None - this is a foundational type definition file.

## Usage

These types are used throughout the library to ensure type safety and provide IntelliSense support for developers using the library.
