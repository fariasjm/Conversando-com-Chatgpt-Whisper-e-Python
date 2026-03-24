# Conversando com Chatgpt, Whisper e Python

Este projeto busca criar um sistema de conversa por voz simples, com inteligência artificial, permitindo que o usuário faça a pergunta, o sistema transcreva a fala para texto, transfira para o ChatGPT e devolva a responda em áudio.

## Recursos utilizados:
  - OpenAI Whisper (Speech-to-Text)
  - ChatGPT (Processamento de linguagem)
  - Google Text-to-Speech (gTTS) e
  - Python

## Reconhecimento de Fala com Whisper
Para interagir com Whisper (OpenAI) instalar a biblioteca openai.

pip install openai

### Exemplo 01: Como utilizar o Whisper para reconhecer fala utilizando o Python.

import openai

openai.api_key = 'YOUR_OPENAI_API_KEY'

def recognize_speech(audio_data, language="en-US"):
    response = openai.SpeechApi.complete(
        model="whisper",
        prompt={
            "audio": audio_data,
            "language": language
        }
    )
    return response['text']

Exemplo de uso:
audio_data = ...  # Aqui você carrega o áudio, por exemplo, de um arquivo de entrada
recognized_text = recognize_speech(audio_data)
print(f"Texto reconhecido: {recognized_text}")


### Exemplo 02: Integração com ChatGPT

def chat_with_gpt(prompt_text, chatbot="gpt-3.5-turbo"):
    response = openai.ChatCompletion.create(
        model=chatbot,
        messages=[
            {"role": "user", "content": prompt_text}
        ]
    )
    return response['choices'][0]['message']['content']

Exemplo de uso:
recognized_text = "Qual é a sua pergunta?"
response_text = chat_with_gpt(recognized_text)
print(f"Resposta do ChatGPT: {response_text}")


### Exemplo 03: Síntese de Voz com gTTS

pip install gtts
from gtts import gTTS
import os

def text_to_speech(text, language='en'):
    tts = gTTS(text=text, lang=language, slow=False)
    tts.save("response.mp3")
    os.system("mpg321 response.mp3")  # Reproduz o arquivo de áudio

Exemplo de uso:
response_text = "Esta é a resposta do ChatGPT."
text_to_speech(response_text)



(Em construção)





