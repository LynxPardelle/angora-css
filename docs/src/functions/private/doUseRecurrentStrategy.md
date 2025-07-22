# doUseRecurrentStrategy - Intelligent CSS Generation Strategy Manager

## Overview

The `doUseRecurrentStrategy` function implements an intelligent CSS generation strategy that manages timing, prevents redundant operations, and coordinates recurrent processing. It serves as the primary controller for the recurrent CSS generation approach, optimizing performance through timing analysis and state management.

## Location

```
src/functions/private/doUseRecurrentStrategy.ts
```

## Dependencies

- `valuesSingleton.ts` - Global state and timing configuration
- `doCssCreate.ts` - Core CSS generation functionality
- `console_log.ts` - Logging and debugging

## Core Function

### doUseRecurrentStrategy()

```typescript
async doUseRecurrentStrategy(
  updateClasses2Create: string[] | null = null,
  primordial: boolean = false,
  recurrent: boolean = false
): Promise<void>
```

Manages CSS generation timing and coordinates recurrent processing with intelligent scheduling.

#### Parameters

- `updateClasses2Create: string[] | null` - Optional array of specific classes to update
- `primordial: boolean` - Flag indicating priority/initial generation (default: false)
- `recurrent: boolean` - Flag indicating this is a recurrent call (default: false)

#### Returns

- `Promise<void>` - No return value (side effect: manages CSS generation timing)

## Processing Logic

### 1. Timestamp Management

```typescript
if (!recurrent) {
  values.lastTimeAsked2Create = Date.now();
}
```

**Initial Requests**
- Updates request timestamp for new (non-recurrent) calls
- Preserves original timestamp for recurrent processing
- Enables timing analysis for scheduling decisions

### 2. Generation Condition Evaluation

```typescript
if ((values.lastTimeCssCreateEnded + values.timeBetweenReCreate < values.lastTimeAsked2Create ||
    primordial === true ||
    values.timesCSSCreated === 0) && !values.cssCreateIsActive) {
  // Execute CSS generation
}
```

**Condition Components**

**Timing Check**
- `lastTimeCssCreateEnded + timeBetweenReCreate < lastTimeAsked2Create`
- Ensures sufficient time has passed since last generation
- Prevents excessive generation frequency

**Priority Override**
- `primordial === true` - Forces immediate generation regardless of timing
- Used for critical updates and initial setup

**First Run**
- `timesCSSCreated === 0` - Always processes first generation request
- Ensures system initialization

**Activity Guard**
- `!cssCreateIsActive` - Prevents concurrent generation operations
- Maintains generation queue integrity

### 3. CSS Generation Execution

```typescript
values.timesCSSCreated++;
values.cssCreateIsActive = true;
const lastTimeCssCreateEnded: number = await doCssCreate.start(updateClasses2Create);
values.lastTimeCssCreateEnded = lastTimeCssCreateEnded;
values.cssCreateIsActive = false;
```

**State Management**
- **Counter Increment**: Tracks total generation operations
- **Activity Flag**: Prevents concurrent operations
- **Timing Update**: Records completion timestamp
- **State Reset**: Clears activity flag after completion

**Execution Flow**
1. Mark generation as active
2. Delegate to core CSS generation
3. Capture completion timestamp
4. Reset activity state

### 4. Recurrent Scheduling

```typescript
doUseRecurrentStrategy(updateClasses2Create, false, true);
```

**Self-Invocation**
- Calls itself with `recurrent: true` flag
- Maintains continuous monitoring
- Processes any pending requests

**Parameter Preservation**
- Maintains original `updateClasses2Create` context
- Forces `primordial: false` for recurrent calls
- Sets `recurrent: true` to prevent timestamp updates

### 5. Postponement Handling

```typescript
else if (!recurrent) {
  console_log.consoleLog("info", { creationPostponed: true });
}
```

**Logging Strategy**
- Only logs postponement for initial requests
- Avoids spam from recurrent monitoring
- Provides visibility into timing decisions

## State Variables Integration

### Timing Configuration

- **`timeBetweenReCreate`** - Minimum interval between generations
- **`lastTimeAsked2Create`** - Timestamp of most recent request
- **`lastTimeCssCreateEnded`** - Timestamp of last completion

### Activity Tracking

- **`cssCreateIsActive`** - Prevents concurrent operations
- **`timesCSSCreated`** - Total generation counter
- **`useRecurrentStrategy`** - Strategy selection flag

## Usage Examples

### Initial CSS Generation

```typescript
// First-time generation (primordial)
await doUseRecurrentStrategy(null, true, false);

// Process specific classes
await doUseRecurrentStrategy(['new-class-1', 'new-class-2'], false, false);
```

### Timing-Based Scheduling

```typescript
// Request made at T=0
await doUseRecurrentStrategy(null, false, false);
// CSS generation executes immediately

// Request made at T=100ms (assuming timeBetweenReCreate=500ms)
await doUseRecurrentStrategy(null, false, false);
// Generation postponed until timing condition is met
```

### Recurrent Monitoring

```typescript
// Initial call starts monitoring
await doUseRecurrentStrategy(null, false, false);
// Automatically schedules recurrent checks
// Each completion triggers another monitoring cycle
```

## Performance Optimizations

### Intelligent Scheduling

- **Timing Analysis**: Prevents excessive generation frequency
- **Activity Guards**: Ensures single-threaded generation
- **Request Coalescing**: Groups multiple requests within timing windows

### Resource Management

- **Memory Efficiency**: Minimal state tracking overhead
- **CPU Optimization**: Prevents unnecessary generation cycles
- **I/O Coordination**: Manages CSS manipulation operations

## Error Handling

### Graceful Degradation

- **State Recovery**: Resets activity flags on completion
- **Timing Fallbacks**: Handles timestamp edge cases
- **Logging Integration**: Comprehensive debugging information

### Concurrency Safety

- **Activity Locking**: Prevents race conditions
- **State Consistency**: Maintains coherent timing state
- **Async Coordination**: Proper async/await handling

## Architecture Integration

### Strategy Pattern Implementation

```
CSS Generation Request → Strategy Selection → doUseRecurrentStrategy → doCssCreate
```

This function implements the recurrent strategy option in the broader CSS generation system.

### Configuration Dependencies

- **Global Timing**: Uses singleton timing configuration
- **Strategy Selection**: Responds to `useRecurrentStrategy` setting
- **State Coordination**: Maintains global generation state

### Integration Points

- **Request Entry**: Receives generation requests from main API
- **Core Delegation**: Calls core CSS generation system
- **State Management**: Updates global timing and activity state

## Comparison with Other Strategies

### vs Timer Strategy

- **Continuous Monitoring**: Always active vs timer-based delays
- **Immediate Response**: Can respond immediately when conditions met
- **Resource Usage**: Higher monitoring overhead but better responsiveness

### vs Direct Strategy

- **Timing Intelligence**: Adds timing optimization vs immediate execution
- **Batching Capability**: Can batch requests vs individual processing
- **Performance**: Better for high-frequency updates

This function represents a sophisticated approach to CSS generation management, balancing responsiveness with performance through intelligent timing analysis and recurrent monitoring.
