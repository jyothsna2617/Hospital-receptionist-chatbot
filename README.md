# Hospital-receptionist-chatbot
I am excited to showcase a hospital receptionist bot that I developed .This intelligent assistant can handle answer frequently asked patient queries, and guide visitors through hospital departments. Built using technologies, e.g., Python, Dialogflow, or Rasa
import pyttsx3
import speech_recognition as sr

# Initialize the text-to-speech engine
engine = pyttsx3.init()

# Function to recognize speech input
def recognize_speech():
    recognizer = sr.Recognizer()
    mic = sr.Microphone()
    with mic as source:
        print("Please say something...")
        recognizer.adjust_for_ambient_noise(source)
        try:
            audio = recognizer.listen(source, timeout=5)  # Adjust timeout as needed (e.g., 5 seconds)
        except sr.WaitTimeoutError:
            print("Timeout. No speech detected.")
            return ""

    try:
        print("Recognizing speech...")
        text = recognizer.recognize_google(audio)
        print(f"You said: {text}")
        return text
    except sr.UnknownValueError:
        print("Sorry, I did not understand that.")
        return ""
    except sr.RequestError:
        print("Sorry, the speech recognition service is unavailable.")
        return ""

# Function to get bot response
def get_bot_response(input):
    responses = {
        "hello": "Hi there! How can I help you today?",
        "hai": "Hello! How can I assist you?",
        "can you tell me the booking details": "Sure, I can help you with booking an appointment. Please provide your name and preferred date.",
        "what are the services provided": "We offer general consultations, emergency services, surgeries, maternity care, pediatric care, and more. What do you need help with?",
        "ok thanks": "You're welcome! Have a great day!",
        "default": "I'm sorry, I didn't understand that. Could you please rephrase?",
        "cost of emergency services": "Rupees 1000. For further details, contact us.",
        "cost of maternity care": "Rupees 800. For further details, contact us.",
        "cost of pediatric care": "Rupees 500. For further details, contact us.",
        "tell me the consultation fee": "Consultation fee is Rupees 500. For further details, contact us."
    }

    normalized_input = input.lower()
    return responses.get(normalized_input, responses["default"])

def main():
    print("Hi, good morning everyone. My name is Jyothsna Devi, and I am from Godavari Global University. I am currently a third-year B.Tech student in the CSE department. Today, I am excited to showcase a hospital receptionist bot that I developed with the help of AIMER's intern page. Let's take a look at how it works.")
    engine.say("Hi, good morning everyone. My name is Jyothsna Devi, and I am from Godavari Global University. I am currently a third-year B.Tech student in the CSE department. Today, I am excited to showcase a hospital receptionist bot that I developed with the help of AIMER's intern page. Let's take a look at how it works.")
    print("Hey, I am your hospital receptionist bot. How can I assist you today?")
    engine.say("Hey, I am your hospital receptionist bot. How can I assist you today?")
    engine.runAndWait()

    while True:
        user_input = recognize_speech()  # Use speech recognition for input

        if not user_input:
            continue  # Continue if no input is recognized

        if "thank you" in user_input.lower():
            engine.say("It's my pleasure")
            engine.runAndWait()
            print("Bot: It's my pleasure")
            continue

        bot_response = get_bot_response(user_input)
        print(f"Bot: {bot_response}")
        engine.say(bot_response)
        engine.runAndWait()

if __name__ == "__main__":
    main()
