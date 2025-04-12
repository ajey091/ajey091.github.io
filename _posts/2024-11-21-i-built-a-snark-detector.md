---
layout: post
title: "I Built a Snark Detector"
date: 2024-11-21
categories: projects
---

You know how they say you attract what you are? Well, turns out I have a knack for attracting snarky people. And honestly, I love it. There's something about that dry, witty humor that just clicks with me. But one day, while bantering with my particularly snarky friends, I had a thought: "Could we actually measure how snarky someone is?"

That's how the Snark Detector was born - a fun little project that combines OpenAI's Whisper for transcription, AssemblyAI for voice analysis, and GPT-4 to give you a snark score. It's like having a snarkiness meter for your conversations!

The Snark Detector is a web application that analyzes audio recordings to detect snarkiness in speech. It combines the power of OpenAI's Whisper for transcription, AssemblyAI for voice analysis, and GPT-4 for snark detection.

The idea for this project came from a real-world challenge I faced in my work as a data scientist. In technical discussions and code reviews, I noticed that sometimes well-intentioned feedback could come across as snarky or condescending, even when that wasn't the intention. This realization led me to explore how we could use AI to help people become more aware of their communication style.

The Snark Detector represents an interesting intersection of natural language processing, audio analysis, and behavioral psychology. It's not just about detecting sarcasm or irony - it's about understanding the subtle ways in which our tone and word choice can affect how our message is received. This is particularly important in professional settings where clear, constructive communication is crucial.

Building this tool presented several interesting challenges:
1. **Audio Processing**: Converting raw audio into meaningful features that could indicate snarkiness
2. **Context Understanding**: Teaching the model to distinguish between genuine snark and other forms of expression
3. **Real-time Analysis**: Making the system responsive enough for practical use
4. **User Experience**: Creating an interface that makes the feedback constructive rather than discouraging

The potential applications of this technology extend beyond just detecting snark. It could be used for:
- Improving workplace communication
- Training public speakers and presenters
- Helping non-native English speakers understand tone and nuance
- Providing feedback for customer service representatives
- Enhancing virtual communication in remote work settings

## How It Works

The Snark Detector is pretty straightforward to use. You record a short audio clip (or upload an existing one), and the tool does its magic:

1. **Audio Processing**: First, we clean up the audio and prepare it for analysis
2. **Transcription**: OpenAI's Whisper converts your speech to text
3. **Voice Analysis**: AssemblyAI analyzes the tone and emotion in your voice
4. **Snark Detection**: GPT-4 looks for snarky patterns in both the text and voice data
5. **Results**: You get a snark score and some fun insights about your communication style

## The Technical Stuff

Here's a quick look at the main components:

```python
# Audio processing and transcription
def process_audio(audio_file):
    # Clean up the audio
    audio = clean_audio(audio_file)
    
    # Transcribe using Whisper
    transcription = whisper.transcribe(audio)
    
    # Analyze voice using AssemblyAI
    voice_analysis = assemblyai.analyze(audio)
    
    return transcription, voice_analysis

# Snark detection
def detect_snark(transcription, voice_analysis):
    # Combine text and voice data
    combined_data = {
        'text': transcription,
        'voice_features': voice_analysis
    }
    
    # Get GPT-4's snark assessment
    snark_score = gpt4.analyze_snark(combined_data)
    
    return snark_score
```

## The Fun Part

The best part about this project? Testing it on my friends! We've had some hilarious results, especially when analyzing our group chat recordings. Some highlights:

- One friend who thought they were being super polite actually scored quite high on the snark meter
- Another friend's "helpful suggestions" turned out to be dripping with snark
- My own attempts at being serious often get flagged as moderately snarky (no surprise there!)

## What's Next?

This is definitely a work in progress, and there's plenty of room for improvement:

- Making the snark detection more nuanced (not all snark is created equal!)
- Adding more fun features like "snarkiest phrase of the day"
- Maybe even a multiplayer mode where you can compare snark levels with friends

## Try It Yourself!

You can find the complete code on [GitHub](https://github.com/ajey091/snark-detector).

*Note: This project requires API keys for OpenAI and AssemblyAI. Make sure to set up your environment variables accordingly.* 