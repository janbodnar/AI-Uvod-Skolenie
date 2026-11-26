# AI-Uvod-Skolenie

AI Úvod - školenie

Ján Bodnár - vyštudované financie - školím Javu, Python a AI

## Harmonogram

- 8.00 - 14.00
- 9.30 krátka prestávka
- 11.00 - 12.00 Obedná prestávka







## OpenAI example

```python
import os

from openai import OpenAI

MODEL = "gpt-6-luna"

if not os.getenv("OPENAI_API_KEY"):
    raise SystemExit("OPENAI_API_KEY is not set in the environment.")

prompt = "Is Pluto a planet?"
if not prompt:
    raise SystemExit("Please enter a prompt.")

client = OpenAI()
response = client.responses.create(
    model=MODEL,
    input=prompt,
)
print(response.output_text)
```
