# How to Call OpenAI API from postman

By now, it’s likely that the majority of people have come across the terms ‘ChatGPT’ and ‘AI’ in various contexts. OpenAI has truly pioneered a revolutionary technology by introducing generative Artificial Intelligence, turning these once-specialized terms into nearly household names. Moreover, it seems that the forthcoming years will unveil even more remarkable surprises, further solidifying OpenAI’s role as the leader in the realm of artificial intelligence.

That is why it’s becoming more and more necessary for us to take advantage of this technology, regardless of our backgrounds.

OpenAI API is a very useful way to integrate the functionality of ChatGPT into our applications. In this blog post, which will hopefully be part of a series on AI, we’re going to get a taste of ChatGPT from the view point of a programmer by directly calling the API version of ChatGPT from postman. Here is the step by step guide:

## Account setup
1. Visit OpenAI website at https://www.openai.com/.
2. Login or create an account by clicking on ‘Log in’ button.

## Retrieve API key
Once logged in, you will be presented with two options: ChatGPT and API. Select the latter.

![image](https://github.com/Firasama29/my-blog/assets/67781796/82ea1972-25ee-4c04-86e1-498c7dded926)

1. Navigate to the API keys section in the top navigation menu.
2. The API key is a unique identifier used to authenticate requests. Click on ‘Create new secret key’ to generate a new key and give it a name. Once generated, copy and keep the key secure to use later to authenticate your requests.
3. Obtain the request body:
  - Navigate to [Playground](https://platform.openai.com/playground) and select [Chat](https://platform.openai.com/playground?mode=chat) mode.

    ![image](https://github.com/Firasama29/my-blog/assets/67781796/04772c11-0b66-491d-a955-3374e618a3a9)

  - Select the desired model (for instance, gpt-3.5-turbo) then type any desired query and click on 'Submit'.
  - Navigate to ‘View Code’ section and copy the displayed curl command.

    ![image](https://github.com/Firasama29/my-blog/assets/67781796/3b93d404-d741-4df5-bc60-76bb1ba84ace)

## Postman setup
1. Launch postman.
1. Select ‘import’ and paste the curl command you copied from OpenAI website. Postman automatically parses the command and extracts information like `headers`, `request body` and `URL` as shown in examples below and populates them into their respective fields.

2. ![image](https://github.com/Firasama29/my-blog/assets/67781796/817d0b8e-cd3f-4ff8-878c-d2fbcfd4ff73)

   - Sample URL if you’ve chosen `gpt-3.5-turbo`:

     `https://api.openai.com/v1/chat/completions`

   - Sample request body:  

     ```json
       {
        "model": "gpt-3.5-turbo",
        "messages": [
          {
            "role": "user",
            "content": "introduce yourself"
          },
          {
            "role": "assistant",
            "content": "Hello! I am an AI language model developed by OpenAI. I am here to assist you with any questions or tasks you may have. How can I help you today?"
          }
        ],
        "temperature": 1,
        "max_tokens": 256,
        "top_p": 1,
        "frequency_penalty": 0,
        "presence_penalty": 0
      }
    ```

3. In the `Headers` tab, you'll notice the `Authorization` field with a given value of `Bearer $OPENAI_API_KEY`. Replace `$OPENAI_API_KEY` with the actual API key you copied earlier as shown below:        

![image](https://github.com/Firasama29/my-blog/assets/67781796/8637f9e8-3f52-4a33-8cd8-42f3419ba15b)

4. This step is crucial because without valid API key, the server will reject the call as it is not be able to verify the authenticity of the request:

    ```json
      {
        "error": {
            "message": "Incorrect API key provided: $OPENAI_***_KEY. You can find your API key at https://platform.openai.com/account/api-keys.",
            "type": "invalid_request_error",
            "param": null,
            "code": "invalid_api_key"
        }
      }
    ```

5. Send the request and you will receive a response from OpenAI API similar to the following example:

   ```json
      {
        "id": "chatcmpl-8a2jxRihbDdSvbaVfvIufuMbfoFIk",
        "object": "chat.completion",
        "created": 1703601033,
        "model": "gpt-3.5-turbo-0613",
        "choices": [
            {
                "index": 0,
                "message": {
                    "role": "assistant",
                    "content": "Hello! My name is [Your Name]. I am a [Your Profession/Title] with [Number] years of experience in [Your Field]. I am passionate about [Your Expertise/Interests], and I am excited to be here to assist you with any questions or tasks you may have. Please let me know how I can be of help to you!"
                },
                "logprobs": null,
                "finish_reason": "stop"
            }
        ],
        "usage": {
            "prompt_tokens": 49,
            "completion_tokens": 74,
            "total_tokens": 123
        },
        "system_fingerprint": null
      }
   ```

That’s it. We have sent a request to ChatGPT using OpenAI API from postman. The response we’re more interested in is the “content” field, which contains the actual reply generated by ChatGPT.

## Summary
To recap, we have obtained the API key from OpenAI website, configured an HTTP request body, URL and headers, including the API key, in postman. successfully sent a request to ChatGPT and received a response which contains, among other things, an id, model and ChatGPT generated content.

If you’re interested to dive deep and learn more, head over to [OpenAI’s Quickstart Tutorial](https://platform.openai.com/docs/quickstart?context=curl) or explore [ChatGPT](https://chat.openai.com/) interface and have fun.

Thanks for reading.
