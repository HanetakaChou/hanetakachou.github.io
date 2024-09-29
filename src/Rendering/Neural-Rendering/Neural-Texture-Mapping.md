# Neural Texture Mapping

The main idea is to represent the 2D texture by the neural network: $\displaystyle \begin{pmatrix} U & V \end{pmatrix} \rightarrow \begin{pmatrix} R & G & B \end{pmatrix}$.  

## Model  

```python
NUM_FREQUENCIES = 16
NUM_NEURONS_PER_HIDDEN_LAYER = 64
NUM_HIDDEN_LAYERS = 5

keras_model = tensorflow.keras.models.Sequential()
keras_model.add(tensorflow.keras.layers.InputLayer(shape=(NUM_FREQUENCIES * 4,)))
for i in range(NUM_HIDDEN_LAYERS):
    keras_model.add(tensorflow.keras.layers.Dense(NUM_NEURONS_PER_HIDDEN_LAYER, activation="relu"))
keras_model.add(tensorflow.keras.layers.Dense(3, activation="linear"))
```

## References  

\[Boksansky 2024\] [Jakub Boksansky. "Crash Course in Deep Learning (for Computer Graphics)." AMD GPUOpen 2024.](https://gpuopen.com/learn/deep_learning_crash_course/)  
