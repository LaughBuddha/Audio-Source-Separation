# Audio Source Separation using deep learning

Objective: Separate a mixture audio track into individual stems corresponding to drums, bass, vocals, and other instruments. Using a classical technique in non-negative matrix factorization and a state-of-the-art deep learning model architecture in open unmix, the above task is acheived.

All the code is implemented in PyTorch and Python. 

Watch video here: https://drive.google.com/file/d/1mQYxrSR_2vEwZfQ6rOPChYq28Bkrh5fx/view \
\
Full Report: [Audio Source Separation.pdf](https://github.com/LaughBuddha/Audio-Source-Separation/blob/master/Audio%20Source%20Separation.pdf)

# Dataset - MUSDB18

MUSDB18 is the largest freely available dataset for source separation till date. It consists of 150 full-length music tracks (totalling 10 hours) from different genres along with their iso- lated drums, bass, vocals and accompaniment stems [5]. The training set is comprised of 100 tracks, with the remaining 50 tracks constituting the test set. Each instance in the dataset is a 44.1kHz stereo track composed of the full mix plus four stems.

# Non deep learning method - Non Negative Matrix Factorization
Non-negative matrix factorization (NMF) is one of the classical methods used to decompose the magnitude of time-frequency distributions in audio processing. 

The fundamental process of NMF is factorizing the matrix V containing the audio data spectrogram into two separate matrices referred to as bases (W ) and activations (H ) respectively. All three matrices V, W, H are non-negative.

V<sub>m x n</sub> = W<sub>m x r</sub>H<sub>r x n</sub>

r = min(m, n) is the number of source components

NP-hard problem and no close form solution

See full implementation [here](https://github.com/LaughBuddha/Audio-Source-Separation/blob/master/NMF_implementation.ipynb)

# Deep Learning method - Open Unmix

Open-Unmix is a deep neural network reference implementation for music source separation.

Open-Unmix is based on a three-layer bidirectional deep LSTM. The model learns to predict the magnitude spectrogram of a target, like vocals, from the magnitude spectrogram of a mixture input. Internally, the prediction is obtained by applying a mask on the input. The model is optimized in the magnitude domain using mean squared error and the actual separation is done in a post-processing step involving a multichannel wiener filter implemented using norbert. To perform separation into multiple sources, multiple models are trained for each particular target. While this makes the training less comfortable, it allows great flexibility to customize the training data for each target source.

See full implementation [here](https://github.com/LaughBuddha/Audio-Source-Separation/blob/master/Open_Unmix_Implementation.ipynb)

# References
1. [MUSDB18 dataset](https://sigsep.github.io/datasets/musdb.html#musdb18-compressed-stems)
2. [NMF](https://www.audiolabs-erlangen.de/content/05-fau/professor/00-mueller/03-publications/2019_LopezSerranoDOM_NMF_DAFx.pdf)
3. [Open Unmix](https://joss.theoj.org/papers/10.21105/joss.01667)
