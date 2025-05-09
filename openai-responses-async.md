## Async usage

Simply import `AsyncOpenAI` instead of `OpenAI` and use `await` with each API call:

```python
import os
import asyncio
from openai import AsyncOpenAI

client = AsyncOpenAI(
    # This is the default and can be omitted
    api_key=os.environ.get("OPENAI_API_KEY"),
)


async def main() -> None:
    response = await client.responses.create(
        model="gpt-4o", input="Explain disestablishmentarianism to a smart five year old."
    )
    print(response.output_text)


asyncio.run(main())
```

Functionality between the synchronous and asynchronous clients is otherwise identical.

## Streaming responses

We provide support for streaming responses using Server Side Events (SSE).

```python
from openai import OpenAI

client = OpenAI()

stream = client.responses.create(
    model="gpt-4o",
    input="Write a one-sentence bedtime story about a unicorn.",
    stream=True,
)

for event in stream:
    print(event)
```

The async client uses the exact same interface.

```python
import asyncio
from openai import AsyncOpenAI

client = AsyncOpenAI()


async def main():
    stream = client.responses.create(
        model="gpt-4o",
        input="Write a one-sentence bedtime story about a unicorn.",
        stream=True,
    )

    for event in stream:
        print(event)


asyncio.run(main())
```
