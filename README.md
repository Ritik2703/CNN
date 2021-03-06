# CNN (Convolutional Neural Network)
# Hare krishna

# Tutorials - https://www.tensorflow.org/tutorials/images/cnn
#             https://missinglink.ai/guides/neural-network-concepts/convolutional-neural-network-build-one-keras-pytorch/
#             https://www.geeksforgeeks.org/introduction-convolution-neural-network/
#             https://machinelearningmastery.com/keras-functional-api-deep-learning/

# Blog - https://towardsdatascience.com/covolutional-neural-network-cb0883dd6529

![cnnn](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2017/10/convolutional_neural_network.png)

![cnn](https://serving.photos.photobox.com/79977386b6c4c5ac1e2ee6e1e5bdd39462462bfd70bfc0acd2af368667960f2f6297eda7.jpg)

![co](https://media.geeksforgeeks.org/wp-content/uploads/neural_net2-300x147.jpeg)

# Convolution - https://medium.com/@bdhuma/6-basic-things-to-know-about-convolution-daef5e1bc411

![cn](https://miro.medium.com/max/580/0*e-SMFTzO8r7skkpc)
![cn2](https://media.geeksforgeeks.org/wp-content/uploads/cnn-2-300x133.jpg)
![cn3](https://media.geeksforgeeks.org/wp-content/uploads/Screenshot-from-2017-08-15-13-55-59-300x217.png)

# Pooling - https://machinelearningmastery.com/pooling-layers-for-convolutional-neural-networks/

![pl](https://media.geeksforgeeks.org/wp-content/uploads/Screenshot-from-2017-08-15-17-04-02.png)
![pl](https://qphs.fs.quoracdn.net/main-qimg-40cdeb3b43594f4b1b1b6e2c137e80b7.webp)


# Flattening - https://www.superdatascience.com/blogs/convolutional-neural-networks-cnn-step-3-flattening
#              https://missinglink.ai/guides/keras/using-keras-flatten-operation-cnn-models-code-examples/


![flt2](https://missinglink.ai/wp-content/uploads/2019/04/Group-5.png)

# full connection

![fc](https://media.geeksforgeeks.org/wp-content/uploads/Screenshot-from-2017-08-15-17-22-40.png)

```
# Convolutional Neural Network

# Importing the libraries
import tensorflow as tf
from keras.preprocessing.image import ImageDataGenerator
tf.__version__

# Part 1 - Data Preprocessing

# Preprocessing the Training set
train_datagen = ImageDataGenerator(rescale = 1./255,
                                   shear_range = 0.2,
                                   zoom_range = 0.2,
                                   horizontal_flip = True)
training_set = train_datagen.flow_from_directory('dataset/training_set',
                                                 target_size = (64, 64),
                                                 batch_size = 32,
                                                 class_mode = 'binary')

# Preprocessing the Test set
test_datagen = ImageDataGenerator(rescale = 1./255)
test_set = test_datagen.flow_from_directory('dataset/test_set',
                                            target_size = (64, 64),
                                            batch_size = 32,
                                            class_mode = 'binary')

# Part 2 - Building the CNN

# Initialising the CNN
cnn = tf.keras.models.Sequential()

# Step 1 - Convolution
cnn.add(tf.keras.layers.Conv2D(filters=32, kernel_size=3, activation='relu', input_shape=[64, 64, 3]))

# Step 2 - Pooling
cnn.add(tf.keras.layers.MaxPool2D(pool_size=2, strides=2))

# Adding a second convolutional layer
cnn.add(tf.keras.layers.Conv2D(filters=32, kernel_size=3, activation='relu'))
cnn.add(tf.keras.layers.MaxPool2D(pool_size=2, strides=2))

# Step 3 - Flattening
cnn.add(tf.keras.layers.Flatten())

# Step 4 - Full Connection
cnn.add(tf.keras.layers.Dense(units=128, activation='relu'))

# Step 5 - Output Layer
cnn.add(tf.keras.layers.Dense(units=1, activation='sigmoid'))

# Part 3 - Training the CNN

# Compiling the CNN
cnn.compile(optimizer = 'adam', loss = 'binary_crossentropy', metrics = ['accuracy'])

# Training the CNN on the Training set and evaluating it on the Test set
cnn.fit(x = training_set, validation_data = test_set, epochs = 25)

# Part 4 - Making a single prediction

import numpy as np
from keras.preprocessing import image
test_image = image.load_img('dataset/single_prediction/cat_or_dog_1.jpg', target_size = (64, 64))
test_image = image.img_to_array(test_image)
test_image = np.expand_dims(test_image, axis = 0)
result = cnn.predict(test_image)
training_set.class_indices
if result[0][0] == 1:
    prediction = 'dog'
else:
    prediction = 'cat'
print(prediction)

```
