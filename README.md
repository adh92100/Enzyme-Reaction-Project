# Enzyme-Reaction-Project
ML model that looks at the compatibility of an enzyme to a reaction sequence 

1. dataset_creation.ipynb
   
This code uses a dataset from https://zenodo.org/record/7530180 named ‘Biocatalysed_reaction_dataset.zip’ in the folder ‘training_dataset’. This set is split into ‘train’, ‘val’ and ‘test’ folders. This code combines each file into one large file just by changing the folder names. This code also makes smaller files to train the data the model on smaller dataset.

2. training_model.ipynb

This code is heavily based on PepPrCLIP Quickstart.ipynb found at https://github.com/SuhaasBhat/PepPrCLIP/blob/main/PepPrCLIP%20Quickstart.ipynb. The main differences is the two inputs which in this case is an enzyme sequence and a reaction SMILE string. The enzyme is tokenized using ESM language learning model and RXNFP. Each token is shaped to the same size of 128 and ran with a batch size of 16. Loss is measured using  same way that PepPrCLIP uses, which is the average of the cross entropies taken as the matrix is normal and transposed. A score between -1 and 1 is found for each reaction and enzyme pair where 1 is a perfect match and -1 is the opposite. Only positive correlating data sets were given to the model to train on.

3. evaluation_model.ipynb

This code runs the test, validation, and training data sets through the model to evaluate its utility at predicting the data it learns from. There is also a random data set that is ran though the model to further test its utility on a data set it has never seen. For each set it finds the mean score, the  standard deviation, the top and bottom 10 scores, and is generated a histogram to show the full spread of the data. No reaction enzyme reaction pairing got a score above 0.9. Unsurprisingly the training dataset did the best with the test set in second, the validation set in third, and the random set doing the worst. This model was only ran with 3500 pairs of enzymes and reactions for the training set, 100 in the test set and 1400 in the validation set. This is a small fraction if the total datasets from ‘Biocatalysed_reaction_dataset.zip’. So, it stands to reason that with more computing time on the larger datasets this model could become much better. 


other things
In the validation set there seems to be a population of pairings that to the model seem to not correlate with each other. This is most likely because the types of reactions in these pairings are so different to the reactions in the training set that to the model, they seem to be not compatible with each other. This is another problem that could be solved with more training. A similar thing could be said about the random dataset. 

 













