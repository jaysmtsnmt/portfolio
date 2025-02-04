# Self Introduction
Hello! I am Jayden Soh, a Year 5 student studying in VJC. 👋

My <ins> passion for engineering started when I was young </ins>, when my father bought an electronics kit for beginners, consisting of a simple Arduino Uno, with basic components such as LEDs 🚨, LCDs & Buttons 🔘. I had just moved to Switzerland then (as my father got a job there), where the <ins>IB curriculum had given me space & time to explore more into that area.</ins> One of my first projects was a very simple door alarm system 🔔, where I had used a button, chopsticks and string to detect the opening of a door! Then, as I gained more experience, <ins>I learnt how to code- in C++ & Python</ins>, which unlocked an entire realm of new possibilities. 

**In Secondary School** (back in Singapore), <ins>I also started to explore leadership</ins>, where I served as a class monitor, peer support leader and on the Prefects' Council Executive Comittee. But outside of all that, the thing I still enjoyed the most was engineering 🛠️. During the holidays (when I had the motivation), I would restart my personal projects- to draw ✏️, tinker 🔨, build and code 💻. Most of my projects started from my imagination, for example- <ins>my companion robot CT-02</ins>, where I really really wanted to recreate Jarvis. (obviously didnt work to that extent), while some are for school competitions, for example- the <ins>Modular Fogponics Greenhouse</ins>. Some of the projects which I worked the hardest on were for school assignments, such as the RC cardboard mariokart. 🚗

But now that I am older, I realise the importance of fueling and keeping this passion, as it will be a great asset for my future. I do not want to lose these skills, and I recognise that the priorities that I set in my JC life will play a crucial role in the development of my engineering passion. 

**Hence, my reason for applying for the Computing course in VJC** is to further develop my skills in this area, be it coding, building or designing, and to <ins>further give me the space & time to grow this passion</ins>.

# Overview of my Projects
Most of my projects are a mix of hardware & computing, using C++ to code for Arduino, and Python to code for software/processing. My projects often start with me building the hardware, then coding the software, as I prefer working with physical materials. 

## Computing & Logic Projects
[CT-02 Companion Robot | 2022 - Current](#ct-02) #Python #C++  

- A companion robot that uses 2D/3D word vectors for natural language processing, as well as opencv & serial modules for face tracking.
- Project started in late 2022

[Autonomous Drone Maze Navigation Code | DSTA YDSP Camp Submission 2023](#dsta-ydsp-camp-submission) #Python #Drone

- Best Obstacle Avoidance Award
- Only one of two teams that were able to navigate out of the maze. (VS & VJC)
- Competition code completetly written from scratch.

[The Unfortunate Tales of Edwun Lim | Chemistry GA Submission 2024](#the-unfortunate-tales-of-edwun-lim) #Scratch #Pixel Art 

- A scratch-based escape room game complete with playable rooms, functioning UI, 2D top-down movement & custom game items.
- Over 50+ hours of time taken to develop
- Submitted for my Y4 Chemistry GA (96% Grade)

## Engineering & Design Projects
[Modular Fogponics Greenhouse | MakeIT Submission 2020](#modular-fogponics-greenhouse) #Design #3D Printing #Lasercutting #Electronics

- MakeIT Communication Award
- A working modular greenhouse prototype consisting of a CPU & Greenhouse module.
- Made using acrylic & 3D printed materials

[Scale Cardboard RC Mariokart | English GA Submission 2023](#scale-rc-mariokart) #Mechanical Engineering #Cardboard #R.C.

- A working scale radio-controlled model Mariokart, made completely out of cardboard.
- Fully designed from scratch with custom servo steering mechanism.
- Submitted for my Y4 English GA

[RC Planes | Switzerland 2017 - 2020]() #Mechanical Engineering #Foamboard #R.C.

- Developed an interest in Aerodynamics & planes
- Trained myself using simulators to fly RC planes
- Built 2 foamboard planes & flew one very regularly

[Lightweight RC Plane | SAFMC Submission 2023]() #Mechanical Engineering #R.C.

[Robotic Arm | Switzerland 2019]() #Mechanical Engineering #C++ 

[Mechanical Keyboards | Singapore 2023]() #Design

# CT-02

<details>
<summary>Picture of CT-02 Version 1 (2022 when I got COVID)</summary>
   
![IMG_0376](https://github.com/user-attachments/assets/8c439e66-e964-4118-ad81-bbdc461614d2)
</details>


CT-02 was inspired by all the Star Wars robots & Jarvis from Iron Man. I wanted to create a robot that could 
1. See it's surroundings
2. Be able to understand speech
3. Be able to help my complete daily tasks, such as music controls, alarm setting, calendar setting etc.
4. Be cute

All of CT-02's code was completely from scratch, and the first version was made when I got COVID and was stuck at home. 

**Here is a video of CT-02 working, showcasing NLP. 2024 (before face tracking was added) (turn up volume to listen!)**

https://github.com/user-attachments/assets/bb454fc6-ccc2-4bae-b8e0-1e1d8d3f98ca

**Here is a video of CT-02 working, showcasing its face tracking ability. 2024**

https://github.com/user-attachments/assets/80b3a136-325e-4948-987f-fc61c2dce9e8

CT is coded in **two languages**, C++ & Python. **C++ is used for the hardware side**, where it is ran completely on the **Arduino Mega**, while **Python is used for the software & processing side**. I have worked on this project on & off since 2022, so I cannot remember how some functions work exactly. 

## Python & Processing
Python is responsible for the following functions:
1. Updating the state of the robot (sleep, idle, awake)
2. **Face detection & tracking** (OpenCV)
3. **Speech detection & isolation** (Whisper, pvporcupine, pydub, wave, pyaudio ++) 
4. **Natural Language Processing & Further Action** (2D Vectors)
5. Action Modules (eg. Spotify, Timers etc..)

A full github repo can be found here: https://github.com/jaysmtsnmt/Python/tree/main/The%20CT%20Project/Modules

<details>
<summary>Natural Language Processing</summary>

## Natural Language Processing
CT-02 understands instructions through the use of word vectors. Similar to sentiment analysis (which I visualise as 1D word vectors), I thought that I could tokenise sentences, and analyse how many times each word is repeated in a given number of sentences, for a specific category of instructions.  
  
My robot has a few categories of instructions it can recieve:  
>1. Timer/Stopwatch
>2. Music Playback
>3. Google
>4. Calendar
>5. Log (video log)
>6. Alarms
>7. Room Control
>8. Robot commands

For performing the same action of playing my spotify music, I may give the following instructions:
>Play my music.  
>Play my spotify.  
>Unpause my music.  
>Play bohemian rhapsody.  
>Start my music playback.  
>Turn on my music.

Based on the repetitions, we can see that although words like, music, spotify, play, start, are commonly used, they are not necessarily used in every sentence. Furthermore, they are also commonly used in other instructions, such as "start my timer", or even "turn on the fan". Using traditional methods, we would have to use many "if" or "else" statements to categorise the requests.  
  
But if we assign each word a vector, with a direction and magnitude, direction pointing to the category it favors, and magnitude showing how much it favors. 
>The more the word is repeated (in a specific category), the higher its magnitude (in that category).

![IMG_4597](https://github.com/user-attachments/assets/71cd9991-2fda-49b4-9bf7-1af3c8c823cc)

Code for vector calculation (list of vectors)  

```Python
def addVectorList(vectors):
    x_forces = []
    y_forces = []

    for vector in vectors: #find the x & y component of each vector
        magnitude, direction = vector
        
        if direction == 360: #just in case
            direction = 0
        if isInRange(0, 90, direction): #quadrant 1 (+x, +y)
            a = 90 - direction
            a = (a/180)*math.pi #convert to radians
            Fx = math.cos(a) * magnitude
            Fy = math.sin(a) * magnitude
        elif isInRange(90, 180, direction): #quadrant 2 (+x, -y)
            a = direction - 90
            a = (a/180)*math.pi #convert to radians
            Fx = math.cos(a) * magnitude
            Fy = -(math.sin(a) * magnitude)
        elif isInRange(180, 270, direction): #quadrant 3 (-x, -y)
            a = 270 - direction
            a = (a/180)*math.pi #convert to radians
            Fx = -(math.cos(a) * magnitude)
            Fy = -(math.sin(a) * magnitude)
        elif isInRange(270, 360, direction): #quadrant 4 (-x, +y)
            a = direction - 270
            a = (a/180)*math.pi #convert to radians
            Fx = -(math.cos(a) * magnitude)
            Fy = math.sin(a) * magnitude
            
        elif direction == 0:
            Fx = 0
            Fy = magnitude
        elif direction == 90:
            Fx = magnitude
            Fy = 0
        elif direction == 180:
            Fx = 0
            Fy = -magnitude
        elif direction == 270: 
            Fx = -magnitude
            Fy = 0
        else:
            print(Fore.RED + "Direction Error" + Fore.RESET)
            
        x_forces.append(Fx)
        y_forces.append(Fy)
        
        #direction cannot be 360 as already adjusted in front
    #Sum of X & Y forces
    x_rf = 0
    y_rf = 0
    for force in x_forces:
        x_rf += force
        
    for force in y_forces:
        y_rf += force
        
    r_magnitude = math.sqrt((x_rf*x_rf)+(y_rf*y_rf)) #pythagoeras theorem
    if r_magnitude != 0:
        #finding the heading/direction via quadrant
        if x_rf > 0: #if resultant x force is positive
            if y_rf > 0: #quadrant 1
                r_direction = 90 - (math.atan(abs(y_rf)/abs(x_rf))/math.pi)*180   
            elif y_rf < 0: #quadrant 2
                r_direction = 90 + (math.atan(abs(y_rf)/abs(x_rf))/math.pi)*180
            else: #equals to zero
                r_direction = 90
        elif x_rf < 0:
            if y_rf > 0: #quadrant 4
                r_direction = (math.atan(abs(y_rf)/abs(x_rf))/math.pi)*180 + 270
            elif y_rf < 0: #quadrant 2
                r_direction = 270 - (math.atan(abs(y_rf)/abs(x_rf))/math.pi)*180
            else: #equals to zero
                r_direction = 270
        else: #x = 0
            if y_rf > 0: 
                r_direction = 0       
            elif y_rf < 0:
                r_direction = 180
                
        return [r_magnitude, r_direction]
    
    else:
        return [0, 0]
```

To train CT to be able to differentiate between sentences of different categories, we just need to feed it a training file with 20-40 example instructions per category! All sentences can be easily generated by ChatGPT, making work very easy.  
Reference Training Text File: [XY_training.txt](https://github.com/user-attachments/files/18641746/XY_training.txt)  
The training function will iterate over each sentence in each category, assigning them magnitudes. (each word has different magnitudes in all 8 directions)  

```Python
def train(loops = 1, cutoff_score = 6): #Number of training loops
    loopnumber = 1
    dictionary_number = -1 #Everytime a header is seen, dictionary_number +1
    n_dictionaries = len(listofdicts)
    
    while loopnumber <= loops:
        loopnumber += 1
        
        #Commence Training for requests
        training_file = open(T_XY_TRAINING, "r", encoding="UTF-8")
        
        #Reading the training file
        for sentence in training_file:
            sentence = sentence.lower()
            
            if sentence.find("///") != -1: #if this is a header line
                sentence = sentence.replace("///", "")
                print(Fore.YELLOW + f"[TTA] Dictionary Training: {sentence}" + Fore.RESET)
                dictionary_number += 1
                
            else:
                if dictionary_number != -1 and dictionary_number < n_dictionaries: #do not allow training to start if start header was not read or if dictionary number exceeds range
                    sentence = sentence.split()
                    
                    for word in sentence:
                        #remove ' from training data and replace with is
                        if word.find("’s") >= 0:
                            if listofdicts[dictionary_number].get("is") != None:
                                listofdicts[dictionary_number]["is"] = listofdicts[dictionary_number]["is"] + 1
                                
                            else:
                                listofdicts[dictionary_number]["is"] = 0
                        
                            word = word.replace("’s", "")

                        if word != "a.m." and word != "p.m.":
                            #remove any punctuation from training data and replace with ""
                            for letter in word:
                                if not (ord(letter) >= 97 and ord(letter) <= 122): 
                                    word = word.replace(letter, "")
                        
                        #writing to dictionary
                        if listofdicts[dictionary_number].get(word) != None: #if it is found in the dictionary!
                            listofdicts[dictionary_number][word] = listofdicts[dictionary_number][word] + 1
                            
                        else: #if it is not, create a new value for it
                            listofdicts[dictionary_number][word] = 0                        
                    
        training_file.close()
        
        for dictionary in listofdicts: #Repeat for all dictionaries
            temp_dict = dict(dictionary)
            print(Fore.LIGHTRED_EX + f"[TTA] Filtering Data..." + Fore.RESET)
            for item in temp_dict:
                if temp_dict.get(item) <= deletion_repetition:
                    dictionary.pop(item)
                    
        for dictionary in listofdicts: #Repeat for all dictionaries
            print(Fore.YELLOW + "[TTA] Scaling Data..." + Fore.RESET)
            for item in dictionary:
                dictionary[item] = dictionary[item]/n_xytrain_sentences

        #Save Dictionary Data
        n = 0
        for dictionary in listofdicts: #Repeat for all dictionaries
            print(Fore.LIGHTGREEN_EX + f"[TTA] Saving Dictionary {n} Data" + Fore.RESET)
            print(dictionary)
            print("\n")
            path = r"C:\Users\delay\OneDrive\Documents\Code & Programs\Visual Studio Code\Python\The CT Project\Modules\Text to Action\Data" + f"\{n}_data.pkl"
            
            with open(path, "wb") as file:
                pickle.dump(dictionary, file)
            file.close()    
        
            n += 1
```


Every time a sentence needs to be categorised, the following function finds the magnitude of each word in every direction (8 magnitudes, 8 directions) & finds it's final vector (1 magnitude, 1 direction). The vector sum of all the words in the sentence will return two values:
>1. The direction (which category)
>2. The magnitude (Confidence score)

With the returning of the confidence score, I also wrote a self-check & training algorithm which can improve its accuracy through retraining. 
______________________________________________
</details>

<details>
<summary>Speech Detection & Isolation</summary>

## Speech Detection & Isolation
   
CT-02 can be woken by saying "Hey CT" or "Yo CT", and this is achieved through the PvPorcupine library, as well as threading. 

```Python
    def wakeword():
        keyword_dictionary = {"1": ["Hey CT", WAKEWORDPATH1], 
                    "2": ["Yo CT", WAKEWORDPATH2]}
        access_key = '5XYibmnYr83z6EscaHDRMx7ERgAnRBf1T71w007c+xADuXcb3PhsOg=='
        keyword_paths = []
        
        # for i, device in enumerate(PvRecorder.get_available_devices()):
        #     print('Device %d: %s' % (i, device))
        #     #Device 0: Microphone (Realtek(R) Audio)
            
        for keyword in keyword_dictionary: 
            keyword_paths.append(keyword_dictionary[keyword][1])
            #print(f'Keywords paths {keyword_paths}')
            
        #creating the porcupine object
        porcupine = pvporcupine.create(
            access_key=access_key,
            keyword_paths=keyword_paths,
            sensitivities=[0.5, 0.5])

        #recording audio
        recorder = PvRecorder(frame_length=porcupine.frame_length, device_index=MIC_ID)
        recorder.start()
        print('[AUDIO] Command Armed... ')

        try:
            while True:
                pcm = recorder.read()
                result = porcupine.process(pcm)
                
                if result >= 0:
                    print(f'[PYTHON] Detected Keyword: {keyword_dictionary[str(result+1)][0]}')
                    wakeEvent.set()
                    
        except KeyboardInterrupt:
            print('[STATE] Forcing Deep Sleep...')
            
        finally:
            recorder.delete()
            porcupine.delete()
            print("[AUDIO] Audio Engine shutdown")

wakeword_thread = th.Thread(target=wakeword)
wakeword_thread.daemon = True
wakeword_thread.start()
wakeEvent = th.Event() #if wakeword is called... 

```
If the wakeword is said, it triggers the threading.Event() - wakeEvent, turning it into a "True" value. This allows CT-02 to check every cycle if the wakeword is called, while still keeping it running in the background.  

The following functions help CT-02 to isolate speech into a single wav file (to be fed into the whisper model). It uses another library that I have forgotton how to use, but it basically measures the spike and dip in volume levels, which allows the code to sense when I stop talking. This only works in a mostly quiet environment, such as my room...

```Python
def audio_callback(indata, frames, time, status): #This is the function for detecting timeout
    global audioWrite
    global initialMillis
    global volume_norm
    volume_norm = np.linalg.norm(indata) * 100
    #print("[VOICE] LEVEL | %.3f" %volume_norm, end="\r")
    
    if volume_norm > SPEECH_DETECTION_LEVEL: #speech detected
        audioWrite = True
        initialMillis = getMillis()
    
    if (getMillis() - initialMillis) > timeoutms and audioWrite == True: #this timeout only triggers if text has already been started saying
        print("\n[VOICE] Phrase Finished!")
        initialMillis = getMillis() #reset back
        audioWrite = False
        speechTimeout.set()
    
    elif (recognizer.stopRecording.is_set() == True and audioWrite == False):
        print("[VOICE] No speech detected")
        waitTimeout.set()
        # stream.stop()
        # stream.close()
        
class recognizer:
    stopRecording = th.Event()
    
    def stop():
        recognizer.stopRecording.set()
    
    #stream is almost like a thread, and hence you need to start and stop it. 
    def recognize():
        global initialMillis
        global audioWrite
        global audiodata
        global path
        #Streaming & PyAudio
        pa = pyaudio.PyAudio()
        pstream = pa.open(
            format=FORMAT,
            channels=CHANNELS,
            rate=RATE,
            input=True,
            frames_per_buffer=FRAMES_PER_BUFFER,
            input_device_index=MICDEVICE
        )

        stream = sd.InputStream(callback=audio_callback)
        #print(sd.query_devices())
        
        initialMillis = getMillis()
        # speechTimeout = th.Event() #after speech waiting for more
        # waitTimeout = th.Event() #waiting for speech

        stream.start()
    
        #initialMillis = getMillis()
        initialMillis = int(getMillis())
        
        # while (getMillis() - initialMillis) < waitforstreamload:
        #     print(initialMillis)
            
        
        #print("[VOICE] Stream Started")
        
        while True:
            if audioWrite == True:
                audiodata.append(pstream.read(FRAMES_PER_BUFFER))
                #print('asda')
                
            elif speechTimeout.is_set(): 
                path = audiosavepath + "\\" + f"detectedspeech.wav" #in voice extraction tests we want to save them as different files for testing, but now we just want to find exactly when we spoke
                obj = wave.open(path, 'wb')
                obj.setnchannels(CHANNELS)
                obj.setsampwidth(pa.get_sample_size(FORMAT))
                obj.setframerate(RATE)
                obj.writeframes(b''.join(audiodata))
                obj.close()
                
                file = AudioSegment.from_wav(path)
                boostedfile = file + AUDIO_BOOST

                boostedfile.export(path, format="wav")
                
                audioWrite = False
                audiodata = []
                
                segments, _= model.transcribe(path, beam_size=5)
                
                for segment in segments:
                    print(f"[STT] Speech Detected: {segment.text.strip()}")
                break #have to remove this later
            
            if recognizer.stopRecording.is_set():
                break

            elif waitTimeout.is_set() or recognizer.stopRecording.is_set():
                break
                
        speechTimeout.clear()
        waitTimeout.clear()
        audioWrite = False
        stream.stop()
        
        try:
            return segment.text.strip()
        
        except UnboundLocalError:
            return None
```

_____________
</details>

<details>
<summary>Face Tracking</summary>

## Face Tracking
   
There are two main parts of face tracking that I learnt through trial and error. 
  
1. Face detection  
2. Calculation of the angle correction & Servo movement

## Face Detection (Python)
Very simple face detection code using opencv is used. This code will find how far the centre of the face is away from a centre region, then send the raw coordinates to arduino side (much lag free & easier) 
  
```Python
vid = cv2.VideoCapture(0, cv2.CAP_DSHOW)
vid.set(cv2.CAP_PROP_FRAME_WIDTH, WIDTH)
vid.set(cv2.CAP_PROP_FRAME_HEIGHT, HEIGHT)

ret, frame = vid.read()
if not ret:
    break

frame = frame[int((HEIGHT/2)-(VISION_Y/2)):int((HEIGHT/2)+(VISION_Y/2)), 0:WIDTH] #FULL WIDTH, HALF HEIGHT
faces = detector(cv2.cvtColor(frame, cv2.COLOR_BGR2RGB))
cv2.circle(frame, (int(WIDTH/2), int(VISION_Y/2)), 20, (0,0,0), 3)

for face in faces:
    count += 1
    x1 = face.left()
    y1 = face.top()
    x2 = face.right()
    y2 = face.bottom()
    
    centrex = (x1 + x2)/2
    centrey = (y1 + y2)/2
    #boxarea = (x2 - x1) * (y2 - y1)
    
    cv2.circle(frame, (int(round(centrex)), int(round(centrey))), 10, (0,0,255), 3)
    cv2.rectangle(frame, (x1, y1), (x2, y2), (0, 255, 0), 3)
    
    face_x = round(centrex)
    face_y = round(centrey)

new_frame_time = time.time() 
fps = 1/(new_frame_time-prev_frame_time)     
if (new_frame_time-prev_frame_time) >= serial_comm_limit:
    prev_frame_time = new_frame_time 
    fps = int(fps) 
    
    if (face_x != 0) or (face_y != 0):
        if (abs(face_x - prev_face_x) > movement_pix_sens):
            Serial.write(f"09/{face_x}")
            print(f"\n[PYTHON] Sent: 09/{face_x} | FPS: {fps}")

            prev_face_x = face_x
```

## Calculation of Angle Correction (Arduino)
By putting the webcam on a piece of paper & mapping the angles, you can find the FOV of the webcam & map each pixel to a specific number of degrees.   

![image](https://github.com/user-attachments/assets/c1e7ee89-e2e6-45c4-be7f-b4cb6d96b65f)

I found that the webcam had a 50 degree FOV, which means that for all 1280 pixels, 1 degree correlates to exactly 25.6 pixels. 

```C++
//Face Tracking
//These two variables are for storing incoming data
char rawdata[20]; //RAWDATA
char* inputdata[20]; //processed data   

while (Serial.available() > 0) { //Check for python data
    Serial.readStringUntil('\n').toCharArray(rawdata, 20);
    tokenise(rawdata, inputdata); //raw data is seperated and stored as inputdata

    //Processing pixel data
    if (strcmp(inputdata[0], trackingcmdtag) == 0){ //Checks if the instruction from Python is for Face Tracking
        face_x = charToInt(inputdata[1]);
        int servoCorr = round((face_x - 640)/25.6); //Read the explanation for these math values below
        int finalAngle = (-1*servoCorr)+asa;
            asa = swrite(asa, finalAngle, tracking_speed); #Uses the custom servo library
        }  
    }
```
Hence, you can have a very simple face tracking algorithm that does not require a back & forth feedback loop. 
____________________________________________________________________________________________________________
</details>

<details>
  <summary>Spotify Integration</summary>

## Spotify Integration
   
CT-02 is able to control my Spotify Playback using the spotipy library. It is also able to search up and play songs, switch devices etc, which are all features that the orignal spotipy library does not provide. 
  
```Python
#For extra info, the login information is stalled in .cache, delete .cache to reload the auth

from time import sleep
import spotipy
from spotipy.oauth2 import SpotifyOAuth

callsignlaptop1 = "laptop"
callsignlaptop2 = "jaydens_laptop"
callsigniPhone1 = "iphone"
callsigniPhone2 = "phone"
callsigntv1 = "tv"
callsigntv2 = "samsung tv"

actuallaptopname = "JAYDENS_LAPTOP"
actualiPhonename = "iPhone"
actualtvname = "TOBEADDED"

scope = "user-read-playback-state,user-modify-playback-state"
sp = spotipy.Spotify(auth_manager=SpotifyOAuth(client_id="-----------------------------",
                                               client_secret="-------------------------------",
                                               redirect_uri="http://localhost:1234",
                                               scope=scope,open_browser=True)) 

def currentlyPlaying(justReturnSongInfo = False):
    data = sp.current_playback(market="US", additional_types=None)
    playbackInfo = ""
    songOnlyPlaybackInfo = ""

    if data != None:
        songdata = data.get("item") #First layer
        currentsong = songdata.get("name") #Second layer information
        songartistsdata = songdata.get("artists") #Third layer information
        #print(songartistsdata)
        songartistsfurtherdata = songartistsdata[0] #Forth layer information
        songartists = songartistsfurtherdata.get("name") #Five layer information
        active_device = getDeviceInfo()
        
        songOnlyPlaybackInfo = f"{currentsong} [{songartists}]"
        playbackInfo = f"[SPOTIPY] Currently playing on {active_device}: {currentsong} [{songartists}]"
        #print(playbackInfo)
        
    else:
        playbackInfo = "[SPOTIPY] Spotify is not currently playing anything..."
        #print("Spotify is not currently playing anything...")
    
    if justReturnSongInfo == True:
        return songOnlyPlaybackInfo
    
    else: 
        return playbackInfo

def getDeviceID(device_name, returnaslist = False):
    deviceID = ""
    data = []
    data = getDeviceInfo(returnalldeviceids=True)
    no_of_active_devices = int(data[0])
    count = 1
    
    device_name = device_name.lower()
    
    if device_name == callsignlaptop1:
        device_name = actuallaptopname
        
    if device_name == callsignlaptop2:
        device_name = actuallaptopname
    
    if device_name == callsigniPhone1:
        device_name = actualiPhonename
        
    if device_name == callsigniPhone2:
        device_name = actualiPhonename
    
    #print(data)
    #print(device_name)
    done = False
    for x in range(no_of_active_devices):
        temp = data[count]
        #print(f"datacount {temp}")
        if temp == device_name:
            count += 1
            deviceID = data[count]
            done = True
            
        elif temp != device_name and done == False:
            count += 3
            #print(temp)
    
    #print(f"DEVICEID {deviceID}")
    if deviceID != "" and returnaslist == False:
        return deviceID
    
    elif deviceID != "" and returnaslist == True:
        #print(f"Device: {device_name} | ID: {deviceID}")
        returndata = [device_name, deviceID]
        return returndata
    
    else:
        #print("Error, Device not found!")
        returndata = ["none", "Device is not active!"]
        return returndata

def getDeviceInfo(returnalldeviceids = False):
    spotifydeviceinfo = [0]
    activeDevices = ""
    
    devicesrawdata = sp.devices()
    devicesdata = devicesrawdata.get("devices")
    #print(devicesdata)
    
    for device in devicesdata:
        spotifydeviceinfo[0] += 1 #number of devices
        
        nameofdevice = device.get("name")
        idofdevice = device.get("id")
        isActive = device.get("is_active")

        spotifydeviceinfo.append(nameofdevice)
        spotifydeviceinfo.append(idofdevice)
        spotifydeviceinfo.append(isActive)
        
    #print(spotifydeviceinfo)
    
    if returnalldeviceids:
        #print(spotifydeviceinfo)
        return spotifydeviceinfo
    
    elif returnalldeviceids == False: 
        count = 1
        for x in range(spotifydeviceinfo[0]):
            deviceName = spotifydeviceinfo[count]
            count += 1
            deviceID = spotifydeviceinfo[count]
            count += 1
            isDeviceActive = spotifydeviceinfo[count]
            count += 1
            
            if isDeviceActive == True:
                activeDevices = activeDevices + str(deviceName)
            
        if activeDevices != "":
            #print(activeDevices)
            return activeDevices
        
        else:
            return "No Active Devices on Spotify..."

def pause():
    if (getDeviceInfo() == "No Active Devices on Spotify..."):
        print("No Active Devices on Spotify...")
    
    elif (currentlyPlaying() == "Spotify is not currently playing anything...") and (getDeviceInfo() != "No Active Devices on Spotify..."):
        print("Spotify is not currently playing.")
    
    elif (currentlyPlaying() != "Spotify is not currently playing anything...") and (getDeviceInfo() != "No Active Devices on Spotify..."):
        try:
            sp.pause_playback()
            print("Spotify Playback Paused...") 
            
        except spotipy.exceptions.SpotifyException:
            print("Spotify Playback is already paused...")
    
    else:
        print("HUH??? Spotify module error btw")
    
def play(song = None, song_artist = None, uridata=None):
    if song!= None:
        songdata = searchSpotifySongData(song, song_artist)
        uridata = songdata.get("uri")
    
    # else: 
    #     songdata = searchSpotifySongData(currentlyPlaying(True))
    #     uridata = songdata.get("uri")
    
    uri = [uridata]
    #if song was not found, uridata = None
    
    
    if (getDeviceInfo() == "No Active Devices on Spotify..."):
        print("No Active Devices on Spotify...")
    
    elif (song != None):
        sp.start_playback(uris=uri)
        print("Spotify Playback Started...")
        sleep(1)
        print(currentlyPlaying())
    else:
        try:
            sp.start_playback()
            print("Spotify Playback Started...")
            sleep(1)
            print(currentlyPlaying())
            
        except spotipy.exceptions.SpotifyException:
            print("Spotify is already playing!")

def switchDevice(device_name, force_play=True):
    device_id = []
    device_id = getDeviceID(device_name, returnaslist=True)
    
    #print(f"device_id[1]{device_id[1]}")
    
    if device_id[1] != "Device is not active!":
        sp.transfer_playback(str(device_id[1]), force_play)
        print(f"Currently playing on {device_id[0]}: {currentlyPlaying(justReturnSongInfo=True)}")
        
    else:
        print(device_id[1])

def searchSpotifySongData(song_name, song_artist=None, numberofresults=1):
    cont = True
    if song_name == "":
        print("No song search query!")
        cont = False
    
    if song_artist == None:
        songquery = song_name
        
    else:
        songquery = f"{song_name}, {song_artist}"
    
    searchResults = []
    returndata = {}
    
    if cont:
        for i in range(numberofresults):
            rawdata = sp.search(songquery, limit=numberofresults, market='SG')
            #print(rawdata)
            tracksraw = rawdata.get("tracks")
            tracksdata = tracksraw.get("items")
            
            try:
                songdata = tracksdata[0] #get first track
                
            except IndexError:
                print(f'Song "{songquery}" was not found!')
                break
            
            songName = songdata.get("name")
            songURI = songdata.get("uri")
            songArtistData = songdata.get("artists")
            songArtistData = songArtistData[0]
            songArtist = songArtistData.get("name")
            songAlbumData = songdata.get("album")
            songAlbum = songAlbumData.get("name")
        
            returndata["name"] = songName
            returndata["uri"] = songURI
            returndata["artist"] = songArtist
            returndata["album"] = songAlbum
            #returndata = [songName, songURI, songArtist, songAlbum]
            searchResults.append(returndata)
                
        if numberofresults == 1:
            return returndata #{'name': "Don't Know Why", 'uri': 'spotify:track:1zNXF2svmdlNxfS5XeNUgr', 'artist': 'Norah Jones', 'album': 'Come Away With Me (Super Deluxe Edition)'}
        
        else:
            return searchResults    
        
    else:
        return {}

def testFeatures():
    print(f"{currentlyPlaying()} \n")
    print(f"{getDeviceInfo()} \n")
    print(f"{getDeviceID('iphone')} \n")
    sleep(2)
    pause()
    sleep(2)
    play("Crossroads by slash")
    sleep(2)
    switchDevice("laptop")
    sleep(5)
    switchDevice("iphone")
    sleep(5)
    switchDevice("laptop")

def addtoQueue(song, song_artist = None):
    songdata = searchSpotifySongData(song, song_artist)
    song_name = songdata.get("name")
    song_artist = songdata.get("artist")
    
    if songdata.get("uri") != None:
        try:
            sp.add_to_queue(songdata.get("uri"))
            print(f'Adding {song_name} [{song_artist}] to the queue!')
            
        except spotipy.exceptions.SpotifyException:
            print("No Active Devices on Spotify...")
            
    else:
        if songdata != {}:
            print(f'Unable to add "{song}" to the queue...')

def skip():
    try:
        sp.next_track()
        print(f"Skipping: {currentlyPlaying(justReturnSongInfo=True)}")
        
        sleep(1)
        print(f"Playing: {currentlyPlaying(justReturnSongInfo=True)}")
        
    except spotipy.exceptions.SpotifyException:
        print("No Active Devices on Spotify...")

def rewind():
    try:
        sp.previous_track()
        sleep(1)
        print(f"Rewinding to: {currentlyPlaying(justReturnSongInfo=True)}")
        
    except spotipy.exceptions.SpotifyException:
        print("No Active Devices on Spotify...")

def getPlaylist():
    data = sp.current_user_playlists(limit=50, offset=0)
    playlists = data.get("items") #items in return
    #print(playlists)
    
    for playlist in playlists:
        print(playlist.get("name"))
        print(playlist.get("id"))

```

  
</details>

## C++/Hardware
The most important segment of the C++ code is to recieve serial commands via USB, understand those serial commands, and execute the actions accordingly, physically changing the state of the robot. The robot a few "body parts"
1. Eyes (Left Blue, Right Blue, Left Red, Right Red) (Red for when CT has nightmares)
2. Heart
3. Neck (Servo)
4. Camera (actual webcam)

I wanted the robot to have a very natural design, so its main body only comprises of one square (head), and a rectangle (body). It's eyes are made out of hotglue (I made a baking paper mold) and has LEDs mounted into it. The blinking of the eyes can be seen as the LEDs blink, but I made it more natural by giving each LED a slight delay from each other. (so it actually looks like it is blinking!) 

A Full Github Repo can be found here: https://github.com/jaysmtsnmt/CT-02  

Here is an early version of CT-02 being awakened by a button press: 

https://github.com/user-attachments/assets/477ec8dc-caa5-402b-8769-e1b38a0be822  

The main file comprises of functions which determine how the robot behaves in sleep mode, idle mode & awake mode. I seperated all of it's body & hardware processing functions into seperate libraries for flexibility. 

<details>
  <summary>Python-C++ Serial Communication</summary>  

  ## Python-C++ Serial Communication

### Commands are sent from Python in this form using the Serial Library.  
  
"11/swrite/115": 
03 - Command Tag for SERVO/NECK  
swrite - servo write with no delay function  
115 - desired angle for servo  

After serial detects a new data input, tokenisers are used to organise the incoming data into char* arrays, where the seperator is '/'.
```C++
//Functions
void tokenise(char data[], char *array[MAX_ARRAYSTORE]){ //Tokenise data into char array
    char* token = strtok(data, seperator);
    int i = 0;
    //Serial.print("[Tokenise] "); 

    while (token != NULL){
        array[i++] = token;
        //Serial.print(i-1); Serial.print("( "); Serial.print(token); Serial.print(" )"); Serial.print(" ");
        token = strtok(NULL, "/");
        //Serial.print(token);
    }

    Serial.println();
}
```
</details>

<details>
<summary>Servo/Neck</summary>

## Servo Neck
   
When you write a specific angle to the servo, it immediately snaps to that angle, making it very unnatural. Hence, by using a delay system, you can make movements smoother and more fluid! 

  ```C++
int swrite(int asa, int angle, int servodelay){
    neck.attach(servopin);

    Serial.print("[SERVO] Start Angle: ");
    Serial.println(asa);

    int wangle = angle - asa;

    //Serial.print("[SERVO] Servo must travel by: ");
    //Serial.println(wangle);

    if (wangle > 0){ //  0    90 >  180 //POSITIVE correction

        for (int x = 0; x < wangle; x++)
        {
            asa += increment;

            //For seeing Writen angles one by one
            //Serial.print("[SERVO] Servo Write: ");
            //Serial.println(int(asa));

            neck.write(int(asa));

            // x += 1;
            delay(servodelay);
        }
    }

    if (wangle < 0){ //Negative correction angle | 0  < 90   180

        wangle = -wangle; //negative to postive

        for (int x = 0; x < wangle; x++){
            asa -= increment;

            //For seeing writen angles one by one
            //Serial.print("[SERVO] Servo Write: ");
            //Serial.println(asa);

            neck.write(int(asa));

            //x += 1;
            delay(servodelay);
        }
    }
    Serial.print("[SERVO] End Angle: ");
    Serial.println(asa);

    neck.detach(); //detatch servo

    return asa;
}
```
</details>

<details>
<summary>Heart Beat</summary>

## Heart Beat
   
A very standard and simple heart beat - emulated using a tiny vibration motor. 

  ```C++
int strength = 170;
int heart = 14;
int period = 50; //Miliseconds

void beat(int s = strength, int p = period){
  pinMode(heart, OUTPUT);
  //Serial.println("[EXECUTE] Heart Beat");

  analogWrite(heart, s);
  delay(p);
  digitalWrite(heart, LOW);
}
 ``` 
</details>

<details>
<summary>Eyes</summary>

## Eyes
   
CT-02 has two types of blinks - a single blink & a double blink. Random delays with predetermined offsets allow the blinking to look much more natural. 

```C++
void blink(int x = blinktime, int b = brightness){ //Pass x as mils closed / Blinktime
    //Serial.println("[EXECUTE] Blink");
    pinMode(le, OUTPUT); //left eye
    pinMode(re, OUTPUT); //right eye
    //pinMode(ler, OUTPUT); //left eye red
    //pinMode(rer, OUTPUT); //right eye red

    int choice = random(0, 3);

    if (choice == 1){
    /*
        //Close Eyes
    digitalWrite(le, LOW);
    delay(nrec);
    digitalWrite(re, LOW);

    delay(x);

    //Open Eyes
    digitalWrite(re, HIGH);
    delay(nrec);
    digitalWrite(le, HIGH);

    delay(x);

    digitalWrite(le, LOW);
    delay(nrec);
    digitalWrite(re, LOW);

    delay(x);

    digitalWrite(le, HIGH);
    delay(nrec);
    digitalWrite(re, HIGH);
    */
        //Close Eyes
        analogWrite(le, offvalue);
        delay(nrec);
        analogWrite(re, offvalue);

        delay(x);

        //Open Eyes
        analogWrite(re, b);
        delay(nrec);
        analogWrite(le, b);

        delay(x);

        analogWrite(le, offvalue);
        delay(nrec);
        analogWrite(re, offvalue);

        delay(x);

        analogWrite(le, b);
        delay(nrec);
        analogWrite(re, b);


    }

    else {

        //Close Eyes
        analogWrite(le, offvalue);
        delay(nrec);
        analogWrite(re, offvalue);

        delay(x);

        //Open Eyes
        analogWrite(re, brightness);
        delay(nrec);
        analogWrite(le, brightness);    
    }


}
```
</details>

______________

# DSTA YDSP Camp Submission
The task of the YDSP Camp competition was to program a Tello Drone that could sucessfully map & autonomously navigate an unknown 5 by 5 maze. Using the matplotlib library that was taught to us, we had successfully mapped a correct route through the maze. 

This is a picture of our team getting the award for Best Obstacle Avoidance. 
  
![20231201-243](https://github.com/user-attachments/assets/483d4ef1-4db4-4517-a4da-880e0edc322d)

More videos & pictures are available in the minimized sections below. 

This code had a few distinct features that allowed us to win:

<details>
   <summary>Obstacle Avoidance & Repositioning</summary>
   
## Obstacle Avoidance & Repositioning

Through trial and error, we realised that a **major failure point** of the drone was its inaccuracy in its movement. Even though it was programmed to move a set distance, there was a lot of drift that caused crashes. Hence, we decided to add code to automatically align the drone to the centre of the mat, if it was too close to a wall. **This is one of the videos showcasing our alignment code during the competition.  **  
  
https://github.com/user-attachments/assets/a06c731d-330c-4349-82e0-64e05064868d

The **align()** function allowed me to align the drone as soon as it takes off, then start the main loop. 
```Python
def align():
    sensorvalue = getTOF()
    if sensorvalue > distancefromwall:
        print("[ALIGN] No wall detected in front, can't align!")
    
    else:
        print("[ALIGN] Aligning with front wall...")
        t.send_rc_control(0, horizontalAligningSpeed, 0, 0)
        time.sleep(2)
        stopMovement()
```
  
For the drone to navigate, it must know if there is a wall in front, at the side, or behind, so that it can determine it's next action. However, **we decided to program an alignment code directly into it**. This had saved our group in the competition, allowing us to get second place. 

```Python
def getWalls():
    leftwall = False
    rightwall = False
    frontwall = False
    returndata = [frontwall, leftwall, rightwall]
    
    frontvalue = getTOF()
    time.sleep(sensortime)
    if frontvalue < tooClose:
        print("[ADJ] Too Close, Moving Back...")
        t.move_back(20)
        time.sleep(aligningTime)
    
    yawLeft90()
    time.sleep(rottime)
    leftvalue = getTOF()
    time.sleep(sensortime)
    if leftvalue < tooClose:
        print("[ADJ] Too Close, Moving Back...")
        t.move_back(20)
        time.sleep(aligningTime)
        
    yawRight90()
    time.sleep(0.1)
    yawRight90() 
    time.sleep(rottime)
    rightvalue = getTOF()
    if rightvalue < tooClose:
        print("[ADJ] Too Close, Moving Back...")
        t.move_back(20)
        time.sleep(aligningTime)
        
    #print(f"{frontvalue}, {leftvalue}, {rightvalue}")
    
    time.sleep(1)
    yawLeft90()
    
    #print(orientation)
    
    if frontvalue < distancefromwall:
        print("[WALL] Front Wall Detected")
        frontwall = True
        returndata[0] = frontwall
    
    if leftvalue < distancefromwall:
        print("[WALL] Left Wall Detected")
        leftwall = True
        returndata[1] = leftwall
        
    if rightvalue < distancefromwall:
        print("[WALL] Right Wall Detected")
        rightwall = True     
        returndata[2] = rightwall
    
    print(f"[WALL] Data: {returndata}")
    return returndata     

```
_______________________
</details>

<details>
   <summary>North Priority</summary>

   ## North Priority
   This part of the code had prevented us from going into a deadend. All other functioning teams except VJC & Victoria School (us) had went into the deadend and depleted their battery life. This video shows the deadend in question:

https://github.com/user-attachments/assets/daa60dcc-3ed4-4c6b-896f-94e589a47931

This is only a part of the code (as there are just many logic statements) 

   ```Python
if walls[0] == True and walls[1] == True and walls[2] == True: #If there is a front, left, and right wall, it is a deadend
    deadEnd = True

elif walls[0] == False: #else if there is no front wall and going forward results in a N orientation
    if getNextOrientation("f") == "N":
        print("[NAVI] Moving Forward")
        action = "f"
        t.move_forward(moveDistance)
        updatePadID() 
        actionCompleted = True
    
    else: #Check for alternative actions
        #Check if any other actions are going N
        if (walls[1] == False and getNextOrientation("l") == "N"): #if no left walls and left turn = N
            print("[NAVI] Moving Left instead of Forward")
            action = "l"
            yawLeft90()
            t.move_forward(moveDistance)
            updatePadID()
            actionCompleted = True

        elif (walls[2] == False and getNextOrientation("r") == "N"): #if no right walls and right turn = N
            print("[NAVI] Moving Right instead of Forward")
            action = "r"
            yawRight90()
            t.move_forward(moveDistance)
            updatePadID()
            actionCompleted = True
        
        #Check if any other actions are NOT N
        elif walls[0] == False and getNextOrientation("f") != "S":
            print("[NAVI] Moving Forward")
            action = "f"
            t.move_forward(moveDistance)
            updatePadID()
            actionCompleted = True
        
        elif walls[1] == False and getNextOrientation("l") != "S": #if no left walls and left turn != S
            print("[NAVI] Moving Left instead of Forward")
            action = "l"
            yawLeft90()
            t.move_forward(moveDistance)
            updatePadID()
            actionCompleted = True
            
        elif walls[2] == False and getNextOrientation("r") != "S": #if no right walls and right turn != S
            print("[NAVI] Moving Right instead of Forward")
            action = "r"
            yawRight90()
            t.move_forward(moveDistance)
            updatePadID()
            actionCompleted = True   
            
        else:
            print(Fore.RESET + Fore.RED + "[NAVI] Unintentional, watch out! Moving Forward" + Fore.RESET)
            action = "f"
            t.move_forward(moveDistance)
            updatePadID()
            actionCompleted = True
```
_______________________
</details>

<details>
   <summary>Print Statements & Organised Code</summary>

## Print Statements & Organised Code
   
I had decided to split different sections of the code into functions, so that it was more organised & readable, allowing me to easily call them in the main function. 

![image](https://github.com/user-attachments/assets/f04050b2-5b3a-494a-805b-7d8ab2119c49)

I also put in many print statements that allowed us to easily debug the code, as well as monitor the drone's progress without having to actually look at it! This photo shows us monitoring the status of the drone on the laptop during the competition.  
  
![20231201-041](https://github.com/user-attachments/assets/14dbe3cb-00af-4e12-ac19-58da292b57f0)
  
This part of the code shows some print statements that gave us an idea of what the drone was doing.   

```Python
                    else: #Find other alternatives
                        if (walls[2] == False and getNextOrientation("r") == "N"): #if there is no right wall and turning right will result in a N direction
                            action = 'r'
                            print("[NAVI] Moving Right instead of Left")
                            yawRight90()
                            t.move_forward(moveDistance)
                            updatePadID()
                            actionCompleted = True
                            
                        elif (walls[1] == False and getNextOrientation("l") != "S"): #If turning left will result in a non S direction
                            action = "l"
                            print("[NAVI] Moving Left")
                            yawLeft90()
                            t.move_forward(moveDistance)
                            updatePadID()
                            actionCompleted = True
                            
                        elif (walls[2] == False and getNextOrientation("r") != "S"):#If turning right will result in a non S direction
                            action = 'r'
                            print("[NAVI] Moving Right instead of Left")
                            yawRight90()
                            t.move_forward(moveDistance)
                            updatePadID()
                            actionCompleted = True
                            
                        else: #No choice but to move left
                            action = "l"
                            print(Fore.RESET + Fore.RED + "[NAVI] Unintentional! Be Careful! Moving Left")
                            yawLeft90()
                            t.move_forward(moveDistance)
                            updatePadID()
                            actionCompleted = True
                                
                else: #If there is no front wall and left wall...
                    if walls[2] == False:
                        print("[NAVI] Moving Right")
                        action = "r"
                        yawRight90()
                        t.move_forward(moveDistance)
                        updatePadID()
```

This part of the code shows the print statements that update us about the obstacles/walls around the drone.
  
```Python
def align():
    sensorvalue = getTOF()
    if sensorvalue > distancefromwall:
        print("[ALIGN] No wall detected in front, can't align!")
    
    else:
        print("[ALIGN] Aligning with front wall...")
        t.send_rc_control(0, horizontalAligningSpeed, 0, 0)
        time.sleep(2)
        stopMovement()

def getWalls():
    leftwall = False
    rightwall = False
    frontwall = False
    returndata = [frontwall, leftwall, rightwall]
    
    frontvalue = getTOF()
    time.sleep(sensortime)
    if frontvalue < tooClose:
        print("[ADJ] Too Close, Moving Back...")
        t.move_back(20)
        time.sleep(aligningTime)
    
    yawLeft90()
    time.sleep(rottime)
    leftvalue = getTOF()
    time.sleep(sensortime)
    if leftvalue < tooClose:
        print("[ADJ] Too Close, Moving Back...")
        t.move_back(20)
        time.sleep(aligningTime)
        
    yawRight90()
    time.sleep(0.1)
    yawRight90() 
    time.sleep(rottime)
    rightvalue = getTOF()
    if rightvalue < tooClose:
        print("[ADJ] Too Close, Moving Back...")
        t.move_back(20)
        time.sleep(aligningTime)
        
    #print(f"{frontvalue}, {leftvalue}, {rightvalue}")
    
    time.sleep(1)
    yawLeft90()
    
    #print(orientation)
    
    if frontvalue < distancefromwall:
        print("[WALL] Front Wall Detected")
        frontwall = True
        returndata[0] = frontwall
    
    if leftvalue < distancefromwall:
        print("[WALL] Left Wall Detected")
        leftwall = True
        returndata[1] = leftwall
        
    if rightvalue < distancefromwall:
        print("[WALL] Right Wall Detected")
        rightwall = True     
        returndata[2] = rightwall
    
    print(f"[WALL] Data: {returndata}")
    return returndata     
```
_______________________
</details>

The full GitHub Archive is available here: https://github.com/jaysmtsnmt/DSTA-YDSP/tree/main/Phase%201 

________________
  
# Modular Fogponics Greenhouse
Designed & submitted for the 2022 MakeIT Design Competition, winning the communication award. I had made this to align with the 30 by 30 Singapore Food Goals, to help increase self-sustainability in Singapore.  
  
This modular greenhouse works using Fogponics, which uses an ultrasonic transducer to create water vapour containing nutrients, which water the plants in the greenhouse!   
>Firstly, This saves a lot more water, and the supply of nutrients can be easily >controlled using a microcontroller (arduino).
  
>Secondly, the prototype's modular snap-on design allows for more greenhouse modules to be connected if needed, while only requiring 1 CPU module. (Modules can be added on any side, and are magnetically coupled.) 

![a97ce2a9-e9e5-46d1-ac44-b38ad78fde42](https://github.com/user-attachments/assets/d63061a2-9474-4e42-af09-a0e9ef371715)
![f26ad2c0-8c64-4029-a8db-08730203ce7d](https://github.com/user-attachments/assets/5aa47d2d-ee8e-491c-86bd-5969751b7f42)

The body of the greenhouse is 0.5 thickness acrylic, while the pots were made out of both acrylic & plastic (3D printed)

## The Design Process

<details>
<summary>The Design Process</summary>

## The Design Process - Design on CAD software
With a vision in mind, I designed the entire greenhouse on tinkercad.  

<details>
<summary>1st Version</summary>
   
   ![Mini greenhouse edit 2 Annotation](https://github.com/user-attachments/assets/238dfef8-4267-4faa-9483-588912ea8626)
   
</details>
<details>
   <summary>2nd & Final Version</summary>
   
![Fogponics 3D Model (0 5 cm thickness) (1)](https://github.com/user-attachments/assets/315e6c1f-a256-49ab-b6ba-910399e59874)
   
![Exploded Fogponics (1)](https://github.com/user-attachments/assets/4f59e198-d4b8-4408-a1ea-2c3583d0ef13)

</details>

## The Design Process - Working with Physical Materials
![image](https://github.com/user-attachments/assets/f2526bdb-bb10-4a4c-aff2-3de091ea93e0)
![image](https://github.com/user-attachments/assets/c3df55b5-c87c-4a0b-b921-ad43b5a8d2a5)

## The Design Process - Testing
In this picture, my laptop was connected to an Arduino Uno, which controlled the ultrasonic transducer module.  
  
![image](https://github.com/user-attachments/assets/949fa3e1-e461-4072-bd3d-4fd72a40b6e4)

In this picture, I was testing the electronics before putting it into the housing. 
  
![A1435004-4BC0-4EA3-A9E6-793953653D20](https://github.com/user-attachments/assets/3b61ac41-8a90-4449-a01e-6b593fce1b32)

## The Design Process - Final Prototype

https://github.com/user-attachments/assets/8c6f6f7f-f0eb-4bbb-b5f5-a45b33dbd92d

![1838922d-4881-402f-bbb6-560bbd881e1b](https://github.com/user-attachments/assets/33adadbd-a34f-49c3-bf73-5572b3fa33ba)

![9fa2ccf9-adb2-469d-a8be-004a12a4342b](https://github.com/user-attachments/assets/75f382bb-fa14-41e5-a4bc-d6fd2e918565)

_________________________   
</details>

## Presentation (Pictures & PDF)

![c162a552-5b7b-4f88-a7dd-1a3908d6be8d](https://github.com/user-attachments/assets/d74f2cbb-9632-4e76-92a9-c98215bbf382)

[MakeIT Presentation.pdf](https://github.com/user-attachments/files/18656936/MakeIT.Presentation.pdf)

________________

# Scale RC Mariokart

For my English GA, our group had choosen **"gaming culture"** as our topic. We had to make an artefact for submission, in which I decided to make a scale RC mariokart, completely from handcut cardboard. I have lost the photo of the fully painted mariokart, but here are some photos and videos showcasing its design.

![image](https://github.com/user-attachments/assets/4c368ba4-df8c-40ec-92e9-934b53d57b8b)

https://github.com/user-attachments/assets/74b200c9-f780-4183-b2ef-f2ff7dba15be

![IMG-20240619-WA0008](https://github.com/user-attachments/assets/b67ef3ef-55a0-4a48-b54e-8e6c10a2fecf)

## The Design Process
There were several steps in the entire process:
<details>
   <summary>Scaling, Designing & Sketching</summary>

   ## Scaling, Designing & Sketching
### Scaling
First, I downloaded a .obj file (3D CAD file) of a mariokart, allowing me to trace it on paper from different angles & get a rough idea of the design.   
   
![IMG-20240619-WA0003](https://github.com/user-attachments/assets/3f0d4ab8-d23f-41c4-8983-16c75c47b10d)

![IMG_4648](https://github.com/user-attachments/assets/8a32b43a-67de-43f4-bc74-ce3457a08f09)

![IMG_4644](https://github.com/user-attachments/assets/261d317c-5eb8-4fa7-a1d6-a19a216c43a8)
  
Eventually, I settled on a ~10:2.1 scale! (not exact because i changed it after) 

### Designing
Next, I started sketching the full dimensions & map of the mariokart, & splitting the cardboard into different sections for easy assembly. 

**One of the problems that I had to solve was the steering system.** The steering system had to be controlled by a single servo, which was connected to a flysky reciever (originally meant for RC planes). To turn a horizontal force into a turning force was not easy, but eventually I settled on this design, which uses stripped & bent metal wires.

https://github.com/user-attachments/assets/266d1524-fe11-48cc-a4b8-5ee5e26574e6

### Sketching

![IMG_4642](https://github.com/user-attachments/assets/a90158f4-747d-43e5-88ad-0008719ad37b)

![IMG_4645](https://github.com/user-attachments/assets/0c3ec660-6dc0-4db4-82d1-e444077a2526)
   
___________
</details>

<details>
   <summary>Experimentation & Finalisation</summary>
   
## Experimentation & Finalisation 
I originally wanted to use a plane brushless motor for driving the mariokart, but it did not have enough torque.  
  
![image](https://github.com/user-attachments/assets/8e478d4b-22b1-4216-aeab-10954b48a4c5)

![image](https://github.com/user-attachments/assets/a7cd52ba-01df-4d98-a8ed-e5bb7a3e1726)

In the end, I had to redesign & rescale the entire mariokart again, as I had to adjust to the normal DC motor specifications. (the wheel was too big)
_______________
</details>

<details>
<summary>Cutting & Assembling</summary>

## Cutting & Assembling

### Cutting the main body

https://github.com/user-attachments/assets/9c623c87-6799-4106-8076-d77ed785f0d3

### Cutting the Wheels

https://github.com/user-attachments/assets/6c4b45a8-a5a5-486d-8ac3-06c7f9b60925

### Assembling
https://github.com/user-attachments/assets/c6c31703-b31d-44ec-b559-05a21e1f388f

![image](https://github.com/user-attachments/assets/5dc220a1-74dd-4989-8779-9bfe594b89a8)

![IMG-20240619-WA0007](https://github.com/user-attachments/assets/ddc29e28-dffb-44e5-a55e-d04828c72360)
_____________________
</details>
<details>
<summary>Electronics & Further Assembling</summary>
   
## Electronics & Further Assembling

https://github.com/user-attachments/assets/4cc6d622-1827-4325-a7c3-7973325f0bc8

![image](https://github.com/user-attachments/assets/e7fb30c2-321e-4ab9-b6ed-90aa02d3d101)
__________________
</details>
<details>
<summary>Testing & Painting</summary>
   ## Testing & Painting
Video of me testing the steering capability of the mariokart!

https://github.com/user-attachments/assets/74b200c9-f780-4183-b2ef-f2ff7dba15be

Picture of my group painting while I add the last touches of cardboard...

![image](https://github.com/user-attachments/assets/32063fdd-b7f7-4e9a-8496-88d98b8b93d7)
___________
</details>
_______________

# The Unfortunate Tales of Edwun Lim
A fully playable scratch game with custom drawn pixel art items. Very overkill for my chemistry GA!  (96% grade was worth it)

![image](https://github.com/user-attachments/assets/c5a2106a-c2a5-46fd-93a2-1526afb9d5b9)

You may view the code or explore the project here:
https://scratch.mit.edu/projects/1048277997/ 


