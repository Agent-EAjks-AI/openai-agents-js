# AI SDK UI Stream Example

This example shows how to convert an Agents SDK streaming run into responses that
are compatible with the AI SDK UI data stream and text stream protocols.

## Run the Next.js chat UI

```bash
pnpm -F ai-sdk-ui-stream dev
```

Open http://localhost:3000 for the UI message stream (tool calls and reasoning
parts are rendered). Open http://localhost:3000/text for the text-only stream.

## Run the Node.js text stream sample

```bash
pnpm -F ai-sdk-ui-stream start:text-stream
```

## Next.js route examples

```ts
import { Agent, run } from '@openai/agents';
import { createAiSdkUiMessageStreamResponse } from '@openai/agents-extensions';

export async function POST() {
  const agent = new Agent({
    name: 'Assistant',
    instructions: 'Reply with a short answer.',
  });

  const stream = await run(agent, 'Hello there.', { stream: true });
  return createAiSdkUiMessageStreamResponse(stream);
}
```

```ts
import { Agent, run } from '@openai/agents';
import { createAiSdkTextStreamResponse } from '@openai/agents-extensions';

export async function POST() {
  const agent = new Agent({
    name: 'Assistant',
    instructions: 'Reply with a short answer.',
  });

  const stream = await run(agent, 'Hello there.', { stream: true });
  return createAiSdkTextStreamResponse(stream);
}
```
