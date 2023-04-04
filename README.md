# GMM_uniform
GMM uniform est package developpé sous python , qui permet de realiser simultanément le clustering et la détection d'outliers.
Le package est constitué d'une classe : GMM_unifrom et une fonction auto_gmm.

## Installation
```sh
pip install gmm_uniform
```

### Classe GMM_uniform : 
**Paramétres** : 
- *k* : le nombre de composantes gaussiennes
- *n_init* :  le nombre d’initialisation aleatoires (20 par defaut). 
- *uniform* : une variable binaire qui indique si une composante uniforme (outliers) sera prise en consideration  ou pas.

**Attributs** :
- *p* : les propoertions de chaque composantes.
- *mean* : la moyenne de chaque composante gausienne.
- *cov* : la convariance de chaque composante gaussienne
- *a* , *b* : parametres de la composante uniforme, si presentes.
- *likelihood_history* : la valeur de la vraisemblance tout au long des iterations de l’algorithme  

**Methodes** : 
- *fit(X)* : estime des parametres du modele en utilisant l'algorithme EM.
- *pobas(X)* : Calcule les probabilités d'appartenance a chaque composante selon les parametres estimés du modele;
- *predict(X)* : Predit les classes d'appartenance à chaque composante.
- *BIC(X)* : Calcule le score BIC du modele sur les données.

**Exemple d'utilisation**:
```python
from gmm_uniform import GMM_Uniform 

gmm_uniform = GMM_Uniform(3, n_init=20, uniform=True)
gmm_uniform.fit(X, max_iter=100)
y_hat = gmm_uniform.predict(X)
print(gmm_uniform.BIC(X))
```

### Fonction auto_gmm : 
**Paramétres** : 
- *X* : Les données.
- *k* : le nombre de composantes gaussiennes
- *n_init* :  le nombre d’initialisation aleatoires (20 par defaut). 

La fonction **auto_gmm** comparera alors un modele gaussien a K composantes avec un modele a K + 1 composantes (K gaussiennes et 1 uniforme). Le meilleur modele selon le critere BIC sera retourné.

**Sorties**: La fonction retourne en sortie sous forme d'un dictionnaire les résultats suivants
 - *uniform_component* : une variable binaire indiquant si le modele avec la composante uniforme a été sélectionné (autrement dit si des outiliers 
sont presents dans les données).
- *probas* : les probabilites d’appartenances de chaque donnée à chaque composante.
- *labels* : l’affectation des donnees aux composantes du mélange.
- *likelihood_history* : pour le modele sélectionné, la valeur de la vraisemblance tout au long des itérations de l’algorithme.
- *BIC* : la valeur du critere BIC.
- *param_proportion, param_means, param_cov* : les parametres du modèle estimé

On fournit dans le notebook suivant une démonstration de l'utilisation de cette fonction avec des données simulées : [Notebook demo](https://colab.research.google.com/drive/1vXohSLkv81su05q-6oIbmNB31U8Hg1wZ?usp=sharing)

## License
GNU General Public License v3
