# TensorFlow LSTM generating video game music

This repository serves as the music-generating side of the game available [here](https://github.com/IngvarBaranin/music-unity).

# Data

All MIDI files used in this project are from [vgmusic.com](vgmusic.com)'s miscellaneous piano only category and are copyrighted by their respective authors. For this reason, the files are not included in this repository. Furthermore, it should be emphasized that this project solely serves a research purpose, not a commercial one.

# Generating music

The generative model is trained by iterating over all MIDI files and encoding them into [tokens describing musical events](https://github.com/IngvarBaranin/ai_music_generation/blob/main/dataset_text/miditokens_waitFix.txt). In preprocessing (done before training in [training-LSTM-generator.ipynb](https://github.com/IngvarBaranin/ai_music_generation/blob/main/notebooks/training-LSTM-generator.ipynb), but not included in repo due to file size), the tokens are preprocessed into a file in the form of 50 token long sequences followed by their subsequent token - using a sliding window algorithm, this results in 1M+ such samples.

Finally, the file of tokens sees its tokens converted into ints, one-hotted and used for training. The intuition is that after training, the model is capable of taking in a 50 token long sequence and predicting what should come next, essentially being an open-minded composer. It is worth mentioning that dropout layers are used so the model would not "predict" the exact musical pieces it trained on. 
