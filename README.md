# Edge Impulse: Audio Classification

## About this project

In this project, I made use of the <a href = "https://www.edgeimpulse.com/"> Edge Impulse</a> platform to create a machine learning model suitable for embedded devices (such as a phone or a microcontroller), which would be able to distinguish between sounds of: music playing, a running faucet, and the sound of "background" noise.


For my data sets, I used my phone to record: 
i) a 5 minute 20 second long audio sample of different open faucets in my flat. I recorded from different angles and distances - sometimes bringing the phone close to the tap, and other times taking it further away (or placing it above/below the tap); and I did this for faucets located in different roooms.
ii) a 5 minute 30 second long sample of songs I randomly played for a few seconds each, on my Spotify.
and
iii) a 3 minute 40 second long sample of background noise, which was predominantly the whirr of my laptop fan.


The whole idea was to have my embedded system identify among 3 different types of sounds: background noise, faucet running, or music.


## Data Processing

After collecting the recordings, I transferred the files to my laptop. Using <a href = "https://www.audacityteam.org/"> Audacity</a>, I opened each audio file, and changed the sampling rate to **16000 Hz**. I selected exactly 1-second windows(1000 ms) of my audio recordings, and exported those 1-second bits into folders with the name of the label for the appropriate recording. I kept sliding the selection window to the next second until I finished exporting all of a particular recording. All the 1-second clips were saved with a Signed 16-bit PCM encoding.

---
I added the faucet and background noise sounds from <a href = "https://www.edgeimpulse.com/"> Shawn Hymel's dataset</a> to buffer my own curated dataset, after I had taken the 1-second samples of each class. This combination of recordings per class, is what constituted my data set - ready for feature extraction and model building.


## Data Upload
On my Edge Impulse page, I created a new project, and headed to the Data Acquisition page. I uploaded my audio, taking all files from one folder (hence one label) at a time. I had it automatically split between training and testing data, and I entered the name for the class of data I had uploaded, and saved the data on the Edge Impulse system. This was repeated for all three data classes.


## Feature Extraction
On the Impulse design page of my Edge Impulse project, I initially added an <a href = "http://practicalcryptography.com/miscellaneous/machine-learning/guide-mel-frequency-cepstral-coefficients-mfccs/"> MFCC(Mel Frequency Cepstral Coefficient) </a> processing block (feature extraction) to a Keras classifier, but for this set of data, it had a hard time with the training.
I then changed the processing block to a <a href = "https://pnsn.org/spectrograms/what-is-a-spectrogram#:~:text=A%20spectrogram%20is%20a%20visual,energy%20levels%20vary%20over%20time."> Spectrogram </a> and had much better results.


