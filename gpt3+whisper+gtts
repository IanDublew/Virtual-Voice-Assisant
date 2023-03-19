
import wave
import openai
import pyaudio
from gtts import gTTS
import os


# Set up OpenAI API credentials
openai.api_key = ""



# Set parameters for audio recording
CHUNK = 1024
FORMAT = pyaudio.paInt16
CHANNELS = 1
RATE = 16000
RECORD_SECONDS = 5

# Initialize PyAudio
p = pyaudio.PyAudio()

# Open audio stream from microphone
stream = p.open(format=FORMAT,
                channels=CHANNELS,
                rate=RATE,
                input=True,
                frames_per_buffer=CHUNK)

print("* recording")

# Record audio for specified time
frames = []
for i in range(0, int(RATE / CHUNK * RECORD_SECONDS)):
    data = stream.read(CHUNK)
    frames.append(data)

print("* done recording")

# Stop audio stream and terminate PyAudio
stream.stop_stream()
stream.close()
p.terminate()

# Save audio to WAV file
filename = "audio.wav"
wf = wave.open(filename, 'wb')
wf.setnchannels(CHANNELS)
wf.setsampwidth(p.get_sample_size(FORMAT))
wf.setframerate(RATE)
wf.writeframes(b''.join(frames))
wf.close()


# Transcribe audio using Whisper
audio_file = open("audio.wav", "rb")
transcribed_text = openai.Audio.transcribe("whisper-1", audio_file)
if "text" in transcribed_text:
    transcription = transcribed_text["text"]
    print(transcription)
else:
    print("Transcription failed")




# Send transcribed text as a query to OpenAI GPT-3 API
response = openai.Completion.create(
    engine="text-davinci-003",
    prompt=transcription,
    max_tokens=3000,
    n=1,
    frequency_penalty=1,
    presence_penalty=1,
    stop=None,
    temperature=0.8,
    top_p=1,best_of=1
)


# Get the response from OpenAI API
api_response = response.choices[0].text

# Print the API response
print(api_response)


# Generate audio from transcript
language = 'en'
tts = gTTS(text=api_response, lang=language)

# Save audio to file
filename = "output.mp3"
tts.save(filename)

# Play audio using default media player
os.startfile(filename)



