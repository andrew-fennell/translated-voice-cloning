# CogNative
## Translated Voice Synthesis

Clone a voice and output speech in another language with the original voice.

## Installation

### 1. Install Python:

  Python 3.9 is recommended.

### 2. Create virtual environment (optional):
  ```python3 -m venv pyvenv```

  Activate virtual environment:
  Windows: ```./pyvenv/Scripts/activate```
  MacOS/Linux: ```source pyvenv/bin/activate```

  Deactivating the virtual environment:
  ```deactivate```

### 3. Install [ffmpeg](https://ffmpeg.org/download.html#get-packages). 

Once installed, extract the folder and add ```<ffmpeg folder path>/bin``` to path.
  
### 4. Install [PyTorch](https://pytorch.org/get-started/locally/):
  1. Pytorch Build: Stable (1.11.0).
  2. Your OS: Pick the OS your environment is running CogNative in (Windows or Linux recommended).
  3. Package: Pick what package installer you are using (pip recommended).
  4. Language: Python.
  5. Compute Platform: CUDA 11.3 recommended. If you don't have a GPU pick CPU.
  
### 5. Install required Python packages:
```pip3 install -r requirements.txt```

### 6. Install [models](https://drive.google.com/drive/folders/1fipYnvRT3vayNuGvhfuX1hL0ZC4mEAfs?usp=sharing).

  Once installed, add the models (*.pt) to ```CogNative/CogNative/models/RTVC/saved_models/default```

### 7. Create Google Cloud credentials:
  1. Follow steps to setup [Google Cloud credentials](https://cloud.google.com/docs/authentication/getting-started).
  2. Add Google Credentials to ```credentials.json``` in the top-level directory. There is currently a file named ```credentials.json.template```, your ```credentials.json``` should match the key/value pairs shown there.

## Usage
Start from the CogNative root directory.

### GUI
To launch GUI, run ```python -m CogNative.testUI.UI```

### CLI
Any necessary flags which are not specified will cause a prompt to be generated which must be answered before continuing. Examples follow.

1) Display Help Message: ``` python -m CogNative.main -help ```
```
CogNative CLI FLags:
    -sampleAudio <PATH>: audio file of voice to clone
    -synType <text, audio>: synthesis mode either given input text or by transcribing audio file
    [-dialogueAudio] <PATH>: for audio synType, audio file of dialogue to speak
    [-dialogueText] <PATH>: for text synType, text string of dialogue to speak
    -out <PATH>: output audio file path
    -useExistingEmbed <y/yes/n/no>: Uses saved embedding of previously used voice samples if enabled and present.
```
2) Generate cloned voice from sample voice and text input:
    ``` python -m CogNative.main -sampleAudio CogNative/examples/MatthewM66.wav -synType text -dialogueText "The turbo-encabulator has now reached a high level of development, and it's being successfully used in the operation of novertrunnions." -out cmdExampleText.wav -useExistingEmbed y ```
``` 
Loaded encoder "english_encoder.pt" trained to step 1564501
Synthesizer using device: cuda
Building Wave-RNN
Trainable Parameters: 4.481M
Loading model weights at CogNative\models\RTVC\saved_models\default\vocoder.pt
Synthesizing...
Clone output to cmdExampleText.wav
``` 

3) Generate cloned voice from sample voice and audio input file: 
    ``` python -m CogNative.main -sampleAudio CogNative\examples\MatthewM66.wav -synType audio -dialogueAudio CogNative\examples\BillMaher22.wav -out cmdExampleAudio.wav -useExistingEmbed n ```
```
Loaded encoder "english_encoder.pt" trained to step 1564501
Synthesizer using device: cuda
Building Wave-RNN
Trainable Parameters: 4.481M
Loading model weights at CogNative\models\RTVC\saved_models\default\vocoder.pt
Loading requested file...
Synthesizing...
Clone output to cmdExampleAudio.wav
```

### AutoTranslate script

To use the AutoTranslate script on Windows, drag and drop an audio file onto the script or place a shortcut to the script in ```%AppData%\Microsoft\Windows\SendTo\``` and use the "Send To" context menu function on an audio file to be translated. In both cases a new .wav file with the orginal filename followed by "Translated" will be placed in the same folder. For other platforms, the same CLI flags should be used but details on context menu integration will vary by what packages are installed. 

## Contributing to the project

- Create your own branch ```git branch yourname-feature-name```
- Pull request with a good explanation of your branch
- Include issues that your pull request is addressing
- Squash and Merge, always.

## Python Styleguide

This style guide is important to make sure that all style matches throughout the project.
To style your code, please use the Black Python styler.

Single file:    ```black <python-file-name>```
All files:      ```black .```

## Credit to Real-Time-Voice-Cloning

This github repository serves as the foundation of our voice cloning module.

[Real-Time-Voice-Cloning](https://github.com/CorentinJ/Real-Time-Voice-Cloning)

See license [here](CogNative/models/RTVC/LICENSE.md).

## Credit to noisereduce

This github repository is used for noise reduction postprocessing on the synthesized output.

[noisereduce](https://github.com/timsainb/noisereduce)

See license [here](https://github.com/timsainb/noisereduce/blob/master/LICENSE)

## Team Members

- Andrew Fennell
- Austin Currington
- Xingjian Hao
- Connor Tisdel
- Jacob Smith
- Aref Sadeghi

