# Virtual-Voice-Assisant

Model uses

This project uses three different technologies to transcribe speech to text, search text query using GPT and give out output and then convert the output to speech:

Whisper:
Whisper is a general-purpose speech recognition model. It is trained on a large dataset of diverse audio and is also a multitasking model that can perform multilingual speech recognition, speech translation, and language identification.
 
CHATGPT:
GPT-3 is a state-of-the-art language model developed by OpenAI. This model is capable of performing a wide range of natural language processing tasks, including speech recognition. For this project, we used a version of the GPT-3 model that was trained on the Whisper dataset. The Whisper dataset consists of speech recorded at very low volumes or whispered speech.


gTTS (Google Text-to-Speech) library
gTTS is a Python library and CLI tool that uses Google Text-to-Speech API to convert text to speech. This library supports several languages and offers various customization options such as voice, speed, and pitch. For this project, we used gTTS to convert the transcribed text to speech and saved the audio as an MP3 file.

