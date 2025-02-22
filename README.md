# cop4331
Processes of Object-Oriented Development

## Artifact Links

[Burndown](https://docs.google.com/spreadsheets/d/1KkA6hShrAnCrGkx6CRnxfXMW4dyEY7O3kqynL3QCU7k/edit?usp=sharing)  
[Backlog](https://docs.google.com/spreadsheets/d/1lPTfQT0mY3Ziemiml-AbQvOLRvhgAgoP-le9dON4xg4/edit?usp=sharing)  
[Sprint 2 Backlog](https://docs.google.com/spreadsheets/d/18DcxK4tz8kdK7szBuFjnQuRactKow3j0830Zlirte2c/edit?usp=sharing)  
[UI Video Demo](https://youtu.be/v-gRfFecyvE)  
[Sprint 3 Backlog](https://docs.google.com/spreadsheets/d/1f2owcjyC_3LZBFHurfBAq7Nc4WHFwSsB524ucwUW_vA/edit?usp=sharing)  
[Presentation Outline](https://drive.google.com/open?id=10oovyY6j0JkVwAiX1C7MBZ-Ag_LYe4o8vJNujiEl9VM)  
[Presentation Slideshow](https://drive.google.com/open?id=1-2qotWVlbLmG0uRq99uuz2RZFGq66Q35oHHyLhKqcMI)  
[Sprint 2 UI Video](https://youtu.be/v-gRfFecyvE)  
[Design Documents](https://github.com/adcrn/cop4331/tree/master/Design%20Documents)  
[Vision Statement](https://github.com/adcrn/cop4331/blob/master/Design%20Documents/vision.txt)  
[Demo Video](https://youtu.be/HijtgZWr3LM)  

## Installation/Requirements
This project requires Python 3+ and makes use of several frameworks, e.g. Flask, Angular, Keras, etc. It assumes you are using a Unix-based system. You'll also probably need to have ffmpeg installed and accessible on your system. To setup your environment, please make a new virtualenv using `python -m venv venv` and then activate it by using `source venv/bin/activate`. Then, run `pip install -r requirements.txt`. Note that you may need to have numpy installed first, as one of the packages' dependencies requires it; you can do that by running `pip install numpy` first.

## Run the App
To run the web app, please open two shells and run the following commands.

First shell:
1. `cd static`
2. `ng serve`

Second shell:
1. `export FLASK_APP=server.py`
2. `flask run`

## Major Components
* A-Frame - visualisation engine
* Angular - app frontend
* Flask - app backend
* Keras - framework for defining our neural networks
* Pandas - data wrangling
* LibROSA - used to generate spectrograms for use in the detection network
* Tensorflow - underlying engine for Keras
* YouTube-dl - used to process YouTube links for download

## Other Stuff
We used the [Free Music Archive](https://github.com/mdeff/fma) to train the genre detection neural network; the `fma_small` dataset was chosen as it contains a total of 8000 30-second tracks balanced across eight (8) genres, including newly popular ones such as electronic(a).

### Preparing the Backend
In order to use the model to predict genres, it must first be trained. Before it can be trained, the dataset must be compiled into a pickle for easy passage to the network. Download your preferred flavor of the FMA dataset and extract it to the desired location. After extraction, change the `AUDIO_DIR` variable in `pickler.py` to the root of extracted dataset. Inspect all of the folders for any files that are 1-2 KB large; this is a sign of broken or corrupted files and will cause the script to stop before it dumps the dataset to a pickle. Adjust all the necessary bits and pieces regarding `GENRES`, `genre_to_index`, and `tracks_dict`. Finally, run `python pickler.py` to create a pickle that will be found at `data.pkl`.

After the pickle has been prepared, run `python trainer.py`. The network will automatically split the pickle into training and validation sets, and will train for a user-defined amount of epochs. Upon completion, the model and its weights will be saved to `models.yaml` and `weights.h5` respectively.