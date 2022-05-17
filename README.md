# PSGE
Official repository for the implementation of **Pure Spectral Graph Embeddings (PSGE)** method.

### Model Formulation
PSGE estimates the user-item interaction matrix as:

$$ \tilde{\mathrm{R}} = D_{\mathcal{U}}^{-\alpha}\mathrm{R}D_{\mathcal{I}}^{-\beta} = \tilde{\mathrm{P}}\tilde{\Lambda}\tilde{\mathrm{Q}}^T $$

$$\hat{\mathrm{R}} = \mathrm{R}D_{\mathcal{I}}^{-\beta}\tilde{\mathrm{Q}}\tilde{\mathrm{Q}}^TD_{\mathcal{I}}^{\beta}$$

$$$$

### Best models hyperparameters
For reproducibility purpose, we report the best hyperparameters found for the models during the Grid search, used to produce ***table 2***:
#### **Movielens1M**
* **BPR:** $l_2=0.0$, $\alpha=0.0001$
* **LightGCN:** convolution depth $=3$, $\alpha=0.001$, $l_2=0$ 
* **PureSVD:** $k=20$
* **EASE:** $l_2=0.1$
* **SGMC:** $k=80$
* **PSGE:** $\alpha=0.3$, $\beta=0.4$, $k=80$
#### **Amazon**
* **BPR:** $l_2=0.00001$, $\alpha=0.001$
* **LightGCN:** convolution depth $=1$, $\alpha=0.001$, $l_2=0.00001$ 
* **PureSVD:** $k=10$
* **EASE:** $l_2=0.1$
* **SGMC:** $k=40$
* **PSGE:** $\alpha=0.3$, $\beta=0.5$, $k=80$
#### **Gowalla**
* **BPR:** $l_2=0.0$, $\alpha=0.001$
* **LightGCN:** convolution depth $=4$, $\alpha=0.001$, $l_2=0.0$ 
* **PureSVD:** $k=1500$
* **EASE:** $l_2 = 0.01$ 
* **SGMC:** $k=1500$
* **PSGE:** $\alpha=0.3$, $\beta=0.4$, $k=1500$
### Requirements
To install all the required packages using the following command:
	
	$ pip install -r requirements.txt

### Datasets
To run the provided code is necessary to download and pre-process the datasets. To download and preprocess the datasets used for the paper run the command:

    $ python create_dataset.py
    
The available Datasets are: **Movielens1M, AmazonElectronics, Gowalla**.
*Note:* The dataset will be preprocessed using the exact random seeds used to obtain the results presented in the paper to let the experiments be completely reproducible.

The datasets will be automatically saved under `~/rsys-datasets` to change the path modify the variable `DATASETS_PATH` in the `constants.py` file.

### Train models 
All the models used in the presented work are under the `model` directory.
Every model has its own folder with inside a python file named `train_model_name.py` which can be used to train the model.
e.g.:

    $ python model/lightgcn/train_lightgcn.py --epochs="1000" --val_every="10" ...

One the best model parameters have been found use `--merge_trainval=True` to evaluate the final model performance.

Available models are: **matrix_factorization_bpr, LightGCN, pureSVD, EASE, SGMC, PSGE**

### Experiments
All the experiments presented in the paper can be reproduced running the corrispective file under the `experiments` folder
* **Figure 1:** `experiments/plot/01_plot_lightgcn_filters.py`
* **Figure 2:** `experiments/02a_plot_span_eigv_through_epoch.ipynb` and `experiments/02b_plot_progressive_span_eigenv.ipynb`
* **Figure 3:** `experiments/03_plot_spectral_model_performace.ipynb`
* **Figure 4:** `experiments/04_plot_psge_pop_acc_tradeoff.ipynb`