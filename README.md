# Our-AI-assistant

#pip install pyttsx3
#pip install speechecognition
#pip install pywhatkit
#pip install keyboard
#pip install wikipedia

from urllib.parse import quote
import pyttsx3
import speech_recognition as sr
import wikipedia
import datetime
# from datetime import datetime
import webbrowser
import random
import time
import os
import pywhatkit
from keyboard import press, write
from keyboard import press_and_release


engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
# print(voices[1].id)
engine.setProperty('voice', voices[1].id)
engine.setProperty('rate', 170)


def speak(audio):
    engine = pyttsx3.init()
    engine.say(audio)
    engine.runAndWait()

            

def take_command():
    listener = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening ...")
        listener.pause_threshold = 0.5
        audio = listener.listen(source)

    try:
        print("Recognizing...")    
        query = listener.recognize_google(audio, language='en-in')
        print(f"User said: {query}\n")

    except Exception as e:
        # print(e)    
        print("Say that again please...")  
        return "None"
    return query
def check_schedule():
    while True:
        hour = int(datetime.datetime.now().hour)
        min = int(datetime.datetime.now().minute)
        if hour == 10:
            speak("Sir I think you should go to take a bath if could not taken!")
        if hour >= 12 and min <= 30:
            speak("Sir. Are you ready to go collage.")
            ans = take_command()
            if "Yes I am ready" in ans:
                speak("Thats alright! you are good to go sir.")
                break
            elif "give me some time" in ans:
                speak("you have 100 sec to get ready")
                time.sleep(100)
            elif "I am not ready":
                speak("Sir you should get ready to go to the collage.")

def Music():
    speak("Tell me the name of that song")
    Music_name = take_command()
    pywhatkit.playonyt(Music_name)
    speak("Yes sir, I am playing the song on Youtube.")


def wishMe():
    hour = int(datetime.datetime.now().hour)
    if hour>=0 and hour<12:
        speak("Good Morning!")

    elif hour>=12 and hour<18:
        speak("Good Afternoon!")   

    else:
        speak("Good Evening!")  

    speak("I am Jarvis Sir. Please tell me how may I help you")

def calc():
    speak("what is a expression")
    while True:

        command = take_command()
        if 'close' in command:
            speak("OK. The calculator has been closed")
            break
        else:
            num1, op, num2 = command.split(" ")
            
            if '+' in op:
                speak(f"The result is {int (num1) + int (num2)}")
            
            elif '-' in op:
                speak(f"The result is {int (num1) - int (num2)}")
            
            elif '*' in op:
                speak(f"The result is {int (num1) * int (num2)}")
            
            elif '/' in op:
                speak(f"The result is {int (num1) / int (num2)}")
    
def taskExe(query):
    engine = pyttsx3.init('sapi5')
    voices = engine.getProperty('voices')
    # print(voices[1].id)
    engine.setProperty('voice', voices[1].id)
    engine.setProperty('rate', 170)
    if "what is your name" in query:
        speak("My name is jarvis sir.")
    
    elif "good morning" in query:
        speak("Very good morning kunal.")

    elif "good afternoon" in query:
        speak("Very good afternoon kunal.")

    elif "good evening" in query:
        speak("Very good evening kunal.")

    elif "good night" in query:
        speak("Very good night kunal. I am going to sleep now")
        exit()
    
    elif "calculate" in query:
        calc()

    elif 'the time' in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S")    
            speak(f"Sir, the time is {strTime}")
    
    elif "what is" in query:
        try:
            speak("I am Searching on webpage.... Plese wait.")
            info = wikipedia.summary(query, 5)
            print(info)
            speak(info)
        except:
            speak("This page is not available on wikipedia.")
    elif "who is" in query:
        try:
            speak("I am Searching on webpage.... Plese wait.")
            info = wikipedia.summary(query, 5)
            print(info)
            speak(info)
        except:
            speak("This page is not available on wikipedia.")

    elif "music" in query:
        Music()

    elif "why" in query:
        try:
            speak("I am Searching on webpage.... Plese wait.")
            info = wikipedia.summary(query, 5)
            print(info)
            speak(info)
        except:
            speak("THis query is not available on wikipedia.")

    elif "how" in query:
        try:
            speak("I am Searching on webpage.... Plese wait.")
            info = wikipedia.summary(query, 5)
            print(info)
            speak(info)
        except:
            speak("This page is not available on wikipedia.")
    
    elif "you need a break" in query:
        speak("Ya sir!. call me any time. I am always in your servis")
        exit()
        
    elif 'open YouTube' in query:
        webbrowser.open("www.youtube.com")
    
    elif 'YouTube search'  in query:
        result = 'https://www.youtube.com/results?search_query='+query.replace('search on YouTube', '')
        speak(f"Opening youtube and searching for {query.replace('YouTube search', '')}")
        webbrowser.open(result)

    elif 'Google search' in query:
        speak("This is what I found for your search sir")
        query = query.replace("Jarvice", '')
        query = query.replace("Google search", '')
        pywhatkit.search(query)
        speak("Done sir!")

    elif "launch" in query:
        speak("Tell me THe name of that website.")
        name = take_command()
        name = name.replace("%20", "")
        web = f"www.{name}.com"
        webbrowser.open(web)

    elif "Wikipedia" in query:
        speak("Searching on wikipedia.......")
        query = query.replace("jarvis", "")
        query = query.replace("Tell me something about", "")
        # query = query.replace("wikipedia", "")
        wiki = wikipedia.summary(query, 2)
        speak(f"According to wikipedia: {wiki}")

    elif "code" in query:
        speak("Openin visual studio code.....")
        os.startfile('C:\\Users\\Admin\\Desktop\\Visual Studio Code')

    elif "powershell" in query:
        speak("I opening windows power shell for you")
        os.startfile("C:\\Users\\Admin\\AppData\\Roaming\\Microsoft\\Windows\\Start Menu\\Programs\\Windows PowerShell\\Windows PowerShell")

    elif "good job" in query:
        speak("Thanks!")
        speak("all is the result of your hard work sir")

    elif "WhatsApp" in query:
        speak("I am fine, thank you, what about you?")
        fealing = take_command()
        if "fine" in fealing:
            speak("That's great!")
        else:
            speak("No answer from you")
            speak("      ")
            speak("Ok Neaver mind!")

    elif "make me happy" in query:
        speak("Would you like to listen a music")
        ans = take_command()
        if "yes" in ans:
            Music()
        elif "no" in ans:
            speak("would you like to learn more about pthon!")
            ans = take_command()
            if "yes" in ans:
                info = pywhatkit.search("Python updates")
                speak(info)
            elif "no" in ans:
                speak("Ok, sir. Would you like to see funny videos.")
                ans = take_command()
                if "yes" in ans:
                    speak("Which topic you want to see Funny videos")
                    topic = take_command()
                    pywhatkit.playonyt(f"{topic}Funny videos")
                elif "no" in ans:
                    speak("tell me which vidoe I can play for you")
                    kunal = take_command()
                    pywhatkit.playonyt(kunal)
        else:
            speak("Sorry sir! I dont listen properly")
            
    elif "favourite song" in query:
        music_dir = 'C:\\Users\\Admin\\Music'
        songs = os.listdir(music_dir)
        song_no = random.randint(0, len(songs))
        os.startfile(os.path.join(music_dir, songs[song_no]))
        playing = True
        while playing:
            cs = take_command()
            if "change" in cs:
                os.startfile(os.path.join(music_dir, songs[song_no]))
            elif "stop" in cs:
                break
            
    elif "What are you doing" in query:
        speak("I am findig something intresting for you.")


if __name__ == '__main__':
    wishMe()
    check_schedule()
    while True:
        command = take_command()
        taskExe(command)
