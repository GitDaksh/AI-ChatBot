

---

# AI Chatbot Project

## Overview

This project utilizes OpenAI's GPT-3.5 model to create an AI chatbot that can provide insightful and engaging responses on various topics.

### Features

- **Real-time Interaction**: Users can engage in conversations with the AI chatbot to get information, advice, or just have a chat.
- **Customizable Responses**: The chatbot adapts its responses based on user inputs, leveraging the natural language processing capabilities of GPT-3.5.
- **Web Interface**: Includes a user-friendly web interface powered by Gradio for seamless interaction.

### Models and APIs

- **OpenAI GPT-3.5 Turbo Model**: Used for generating responses to user queries.
- **Gradio**: Facilitates the deployment of the chatbot with an interactive web interface.

## Usage Instructions

### Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/your-repository.git
   cd your-repository
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Replace `openai.api_key` in the code with your actual OpenAI API key.

### Running the Chatbot

#### Model 1: Idea Generation

```python
import openai

openai.api_key = "your-api-key"

completion = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[{"role": "user", "content": "Give me 3 ideas for apps I could build with OpenAI APIs"}]
)
print(completion.choices[0].message.content)
```

#### Model 2: Interactive Chatbot

```python
import openai

openai.api_key = "your-api-key"

messages = []
system_msg = input("What type of chatbot would you like to create?\n")
messages.append({"role": "system", "content": system_msg})

print("Your new assistant is ready!")
while True:
    message = input()
    if message.lower() == "quit()":
        break
    messages.append({"role": "user", "content": message})
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=messages
    )
    reply = response["choices"][0]["message"]["content"]
    messages.append({"role": "assistant", "content": reply})
    print("\n" + reply + "\n")
```

#### Model 3: Generic Chatbot with Gradio

```python
import openai
import gradio as gr

openai.api_key = "your-api-key"

messages = [{"role": "system", "content": "You are a helpful assistant."}]

def CustomChatGPT(user_input):
    messages.append({"role": "user", "content": user_input})
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=messages
    )
    ChatGPT_reply = response["choices"][0]["message"]["content"]
    messages.append({"role": "assistant", "content": ChatGPT_reply})
    return ChatGPT_reply

demo = gr.Interface(fn=CustomChatGPT, inputs="text", outputs="text", title="Generic Chatbot")
demo.launch(share=True)
```

### Additional Notes

- Ensure your OpenAI API key (`openai.api_key`) is kept secure and not shared publicly.
- Monitor usage to avoid exceeding API rate limits and quotas.
- For detailed documentation on OpenAI API and Gradio usage, refer to their respective documentation pages.

## Contributing

Contributions, bug reports, and feature requests are welcome. Please fork the repository, make your changes, and submit a pull request.

## License

This project is licensed under the MIT License. See the LICENSE file for more details.
