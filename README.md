### Python Project to Convert PDF Text to AudioBook & Speech to PDF

This Python project involves converting text in a PDF into speech and converting speech into a PDF. This allows you to listen to books or convert audio files back into text for PDF creation. The project uses libraries like **Tkinter**, **Pydub**, **PyPDF4**, **pyttsx3**, and **SpeechRecognition**.

#### Project Steps:

1. **Importing Required Modules**:
   - `Tkinter`: For GUI creation
   - `Path`: For handling file paths
   - `PyPDF4`: For reading and writing PDFs
   - `pyttsx3`: For text-to-speech conversion
   - `SpeechRecognition`: For speech-to-text conversion
   - `Pydub`: For audio file modification

2. **Converting PDF Text to Speech**:
   - The user selects a PDF and provides page range inputs.
   - The `PdfFileReader` extracts text from the PDF, and `pyttsx3` reads it out loud.
   
3. **Creating the GUI for PDF to Audio Conversion**:
   - Users input start and end page numbers.
   - Upon clicking the button, the PDF is read and converted to audio.

4. **Converting Audio to PDF**:
   - The audio file is selected by the user.
   - Using `SpeechRecognition`, the audio is converted into text and saved into a PDF.

5. **Creating the Main GUI Window**:
   - The main window provides options to either convert PDF text to speech or convert audio back into PDF.

#### Example Code:

```python
import tkinter
from tkinter import filedialog
from path import Path
from PyPDF4.pdf import PdfFileReader, PdfFileWriter
import pyttsx3
from speech_recognition import Recognizer, AudioFile
from pydub import AudioSegment
import os

# PDF to Speech Conversion
def read_pdf():
    path = filedialog.askopenfilename()  # Select PDF
    pdfLoc = open(path, 'rb')
    pdfreader = PdfFileReader(pdfLoc)
    speaker = pyttsx3.init()
    start = start_pgNo.get()  # Start page
    end = end_pgNo.get()  # End page
    for i in range(start, end+1):
        page = pdfreader.getPage(i)
        text = page.extractText()
        speaker.say(text)
        speaker.runAndWait()

# Audio to PDF Conversion
def convert_audio_to_text():
    path = filedialog.askopenfilename()  # Select audio file
    audioLoc = open(path, 'rb')
    audioFileName = os.path.basename(audioLoc).split('.')[0]
    audioFileExt = os.path.basename(audioLoc).split('.')[1]
    if audioFileExt != 'wav' and audioFileExt != 'mp3':
        messagebox.showerror('Error!', 'Audio file should be in .mp3 or .wav format.')
    if audioFileExt == 'mp3':
        audio_file = AudioSegment.from_file(Path(audioLoc), format='mp3')
        audio_file.export(f'{audioFileName}.wav', format='wav')
    # Recognize speech and save as text in a PDF
    recognizer = Recognizer()
    with AudioFile(f'{audioFileName}.wav') as source:
        speech = recognizer.record(source)
    text = recognizer.recognize_google(speech)
    write_text(text)

def write_text(text):
    writer = PdfFileWriter()
    writer.addBlankPage(72, 72)
    with open('output.pdf', 'wb') as output:
        writer.write(output)
        output.write(text.encode())

# Main Window with Buttons
def main_window():
    wn = tkinter.Tk()
    wn.title("PDF to Audio and Audio to PDF Converter")
    wn.geometry('700x300')
    wn.config(bg='LightBlue1')
    
    # Button for PDF to Audio Conversion
    Button(wn, text="Convert PDF to Audio", bg='ivory3', font=('Courier', 15), command=read_pdf).place(x=230, y=80)
    
    # Button for Audio to PDF Conversion
    Button(wn, text="Convert Audio to PDF", bg='ivory3', font=('Courier', 15), command=convert_audio_to_text).place(x=230, y=150)
    
    wn.mainloop()

main_window()
```

### Summary:
This project provides a GUI to either convert PDF text to speech or speech to a PDF. It combines multiple libraries like Tkinter for the interface and pyttsx3 and SpeechRecognition for the conversion functionalities. The project is useful for users who need accessibility features or prefer listening to texts.
