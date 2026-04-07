# Assistant Chat Command Queue

## Purpose

Define the shared assistant design pattern for AI-triggered system actions that should be executed asynchronously and reported back into the chat thread.

## When To Use

- A user asks the assistant to make a system change
- The requested action should not be executed directly in the conversational request path
- The action may take time, fail, or require retry logic
- The system needs durable tracking of AI-requested operations

## Core Pattern

When chat asks the system to perform an action:

1. The assistant creates a command record and places it onto a `chat-commands` queue.
2. A background process picks up the command and performs the requested work.
3. The background process reports completion or failure back to the chat thread.
4. The assistant informs the end user that the command was sent and that it will report back when processing finishes.
5. If the command fails, the assistant may send follow-up commands to resolve the issue.
6. If the issue persists after a second attempt, the assistant informs the end user and waits for further instructions.

## Design Goals

- Avoid blocking the chat request on long-running work
- Preserve user trust through explicit status updates
- Keep AI-triggered system actions auditable
- Support retryable operational workflows

## Core Components

- Chat thread
- Chat message history
- Chat command record
- `chat-commands` queue
- Background processor
- Command status reporting

## Flow

### Request Phase

- The user asks the assistant to perform an action
- The assistant translates the action into a command
- The command is queued rather than executed inline

### Processing Phase

- The background processor executes the command
- Status, success, and failure details are captured

### Completion Phase

- The chat thread is updated with the result
- The assistant informs the user of completion or failure

### Failure Handling Phase

- The assistant may issue a follow-up command to resolve the issue
- If the issue persists a second time, the assistant reports the failure and stops retrying

## Governance Boundaries

- Human-visible actions should be traceable to a command
- Sensitive operations may require explicit approval before queuing
- System behavior should be auditable and reviewable

## Implementation Notes

- Use durable storage for queued command state
- Keep command payloads explicit and versionable
- Keep chat-thread status updates user-readable
- Distinguish between requested action, queued action, processing result, and retry result
