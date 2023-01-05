# Coins images classification using Deep Learnig


Collecting is a broad market which extends to many products, one particular one is the coins collecting, where you can find that one "fiat" coin could be worth 100 times more. Manufacturing defects, antiquity or symbolic creation batchs are one many features collectors value and that are one of the reasons why they are so scarce. 

In the EU, each coin is represented by the indicative value of itself (1€, 2€..) and, on the other side, it is shown a symbol referring to the country where it has been manufactured, but this is not always true. And that are the Conmemorative coins.

A Conmemmorative coin is an special coin a EU country manufactures with the purpose to celebrate or recognise an important event in its history, they have normally low manufacturing batches and, for this reason, some of them are really valued in the market.

On this point is when we want to make a contribution to the society, by creating an algorithm that can show us, by a photo taken to a coin, if this coin is conmemorative and provinding some details about it.

## Data Collection and Selection

We will try to focus into a model that can determine with enough precision between 4 coins images. The ones that we are going to differentiate are 4 "2 euro" coins, 3 Conmemorative and 1 "national" coin.

![ey](https://raw.githubusercontent.com/NotCorrectlyDonated/Learning_Deeply_about_currencies/main/coin%20types/Atenas0%20(78).jpg)
<sub>Conmemorative Athens 2004</sub>

![ey](https://raw.githubusercontent.com/NotCorrectlyDonated/Learning_Deeply_about_currencies/main/coin%20types/Francia0%20(2).jpg)
<sub>France National</sub> 

![ey](https://raw.githubusercontent.com/NotCorrectlyDonated/Learning_Deeply_about_currencies/main/coin%20types/image005.jpg) 
<sub>Conmemorative Pontifica 2006</sub>

![ey](https://raw.githubusercontent.com/NotCorrectlyDonated/Learning_Deeply_about_currencies/main/coin%20types/image007.jpg)
<sub>Conmemorative Altamira 2015 </sub>



Our first approach will be to obtain as much images we can in order to train the model as much as possible, and this is when one of the difficulties comes up. Due to the novelty of the project, there are not many databases englobing images of the "heads" of coin types, and it get even worse when talking about conmemorative coins.

To get as much data as possible, we will rely on one of our previous projects, Web Scrapping with Google Images. (You can see it [here](https://github.com/NotCorrectlyDonated/Google_Images_Scraping) ). 
**Note: This project is made as a first approach, as we are concerned that some of the images obtained are erractic, with low quality or in digital form, which will definetly affect the model (even worse if we have a low quantity of images)**
I managed to obtain a total of 500 images, well balanced between 4 types.

## Data wrangling

Once we have uploaded the images from our local directory, created a dataframe and classified their types (target) we will need to sample the data (to get the algorithm to learn indifferently from all of them) and divide it into train, test and validation.

## Increase the data 
As with just only 500 images divided in 4 classes is highly insufficient for a sequential model to learn, we will use ``ImageDataGenerator`` library to "reorganize" each photo during every Epoch, by rotating, zooming, changing heigth... So the database will increase the information potentially for the algorithm [^1].

We will also take advantage of this library to reescale the images, as this is how the keras model will be optimized.

[^1]: Note that effects such as mirror will not have sense since the heads coins always face the same side.

## Keras Sequential Model

To develop an optimal algorithm I rely on a convolutional neural model, with 2 Convolutional 2D layers of 4x4 (activation in ``relu`` to avoid overfitting) and both a pool size of 3x3. The last layers are the Flatten one, the first one with 128 neurons (also with ``relu`` activation) and finally the exit with 4 neurons (as they are the 4 class) with ``softmax`` activation (as it is optimal for classes)

![ey](https://raw.githubusercontent.com/NotCorrectlyDonated/Learning_Deeply_about_currencies/main/info/Keras%20graph.png)
<sub> Keras model used </sub> 

### Metrics

As we want to reduce the quantity of coins which are wrongly addressed, we will rely on **Recall** and also **CategoricalCrossentropy** as loss metric.


