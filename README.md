# Self Introduction
Hello! I am Jayden Soh, a Year 5 student studying in VJC. 👋

My <ins> passion for engineering started when I was young </ins>, when my father bought an electronics kit for beginners, consisting of a simple Arduino Uno, with basic components such as LEDs 🚨, LCDs & Buttons 🔘. I had just moved to Switzerland then (as my father got a job there), where the <ins>IB curriculum had given me space & time to explore more into that area.</ins> One of my first projects was a very simple door alarm system 🔔, where I had used a button, chopsticks and string to detect the opening of a door! Then, as I gained more experience, <ins>I learnt how to code- in C++ & Python</ins>, which unlocked an entire realm of new possibilities. 

**In Secondary School** (back in Singapore), <ins>I also started to explore leadership</ins>, where I served as a class monitor, peer support leader and on the Prefects' Council Executive Comittee. But outside of all that, the thing I still enjoyed the most was engineering 🛠️. During the holidays (when I had the motivation), I would restart my personal projects- to draw ✏️, tinker 🔨, build and code 💻. Most of my projects started from my imagination, for example- <ins>my companion robot CT-02</ins>, where I really really wanted to recreate Jarvis. (obviously didnt work to that extent), while some are for school competitions, for example- the <ins>Modular Fogponics Greenhouse</ins>. Some of the projects which I worked the hardest on were for school assignments, such as the RC cardboard mariokart. 🚗

But now that I am older, I realise the importance of fueling and keeping this passion, as it will be a great asset for my future. I do not want to lose these skills, and I recognise that the priorities that I set in my JC life will play a crucial role in the development of my engineering passion. 

**Hence, my reason for applying for the Computing course in VJC** is to further develop my skills in this area, be it coding, building or designing, and to <ins>further give me the space & time to grow this passion</ins>.

# Overview of my Projects
# CT-02
CT-02 was inspired by all the Star Wars robots & Jarvis from Iron Man. I wanted to create a robot that could 
1. See it's surroundings
2. Be able to understand speech
3. Be able to help my complete daily tasks, such as music controls, alarm setting, calendar setting etc.
4. Be cute

https://github.com/user-attachments/assets/bb454fc6-ccc2-4bae-b8e0-1e1d8d3f98ca

CT is coded in two languages, C++ & Python. C++ is used for the hardware side, where it is ran completely on the Arduino Mega, while Python is used for the software & processing side. I have worked on this project on & off since 2022, so I cannot remember how some functions work exactly. 

## Python & Processing
Python is responsible for the following functions:
1. Updating the state of the robot (sleep, idle, awake)
2. **Face detection & tracking** (OpenCV)
3. **Speech detection & isolation** (Whisper, pvporcupine, pydub, wave, pyaudio ++) 
4. **Natural Language Processing & Further Action** (2D Vectors)
5. Action Modules (eg. Spotify, Timers etc..)

<details>
<summary>Natural Language Processing</summary>
   
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
1. Eyes (Left Blue, Right Blue, Left Red, Right Red)
2. Heart
3. Neck (Servo)
4. Camera (actual webcam)

I wanted the robot to have a very natural design, so its main body only comprises of one square (head), and a rectangle (body). It's eyes are made out of hotglue (I made a baking paper mold) and has LEDs mounted into it. The blinking of the eyes can be seen as the LEDs blink, but I made it more natural by giving each LED a slight delay from each other. (so it actually looks like it is blinking!) 

Here is an early version of CT-02 being awakened by a button press: 

https://github.com/user-attachments/assets/477ec8dc-caa5-402b-8769-e1b38a0be822  

The main file comprises of functions which determine how the robot behaves in sleep mode, idle mode & awake mode. I seperated all of it's body & hardware processing functions into seperate libraries for flexibility. 

<details>
  <summary>Python-C++ Serial Communication</summary>  

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
