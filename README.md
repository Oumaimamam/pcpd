# Projet : Couverture de Produits dérivés

## 1. **Objectif:**

Un projet de pricing et de couverture en Delta de produits dérivés: Options (Basket, Performance, Asian).

### - **Le pricing:**

On modélise la dynamique de diffusion du sous-jacent par un modèle de Black-Scholes :

$$
S_{t,d} = S_{0,d} e^{\left(r - \frac{\sigma_d^2}{2}\right)t + \sigma_d B_{t,d}}, \quad d = 1, \dots, D
$$

On estime ensuite le prix de l'option par **Monte Carlo**.

### - **La couverture:**

On utilise une couverture en delta pour nos stratégies. Ceci dit qu'on calcule les sensibilités (deltas) du prix de l'option par rapport au sous-jacent, pour construire un portefeuille de couverture avec des quantités delta de chacun des actifs sous-jacents.

Les deltas :

$$
\frac{\partial v(t, S_{t_0}, \dots, S_{t_i}, S_t)}{\partial S_t}
$$



## 2. **Env du Dev:**

-   **Installation du `PNL`:**

```bash
mkdir lib
cd lib
cp /relative/path/to/pnl ./
mkdir build
cd  build
cmake ..
chmod +x ../split_linker_command.sh
make
make install
```

-   **Installation du `nlohmann-json`:**

```bash
sudo apt update
sudo apt install nlohmann-json3-dev
```

-   **compilation:**

```bash
mkdir build
cd build
cmake -DCMAKE_PREFIX_PATH=relative/path/to/lib/pnl/build/ ..
make
```

- **Execution:**

```bash
./price0 data_input.json
./hedge market_file.txt data_input.json
```

-   **configuration vscode:**

    -   Ouvrir le fichier `c_cpp_properties.json`
    -   Ajouter dans `includePath`: **`"relative/path/to/lib/pnl/build/include/"`**

-   **Ajouter un executable dans `CMakeLists.txt`:**

```Makefile
add_executable(nomExecutable _liste_des_fichiers_cpp)
target_link_libraries(nomExecutable
    ${PNL_LIBRARIES}
    nlohmann_json::nlohmann_json
)

```

-   **Tests:**

```bash
python3  ./CheckArchive.py --check --extract --destdir=tests_rendu/rendu/  --build --pnldir=lib/pnl/build/  tests_rendu/Equipe_2.tar.gz
python3 ./testForPCPD.py --price --exec=tests_rendu/rendu/Equipe_2/build/price0  --datadir=tests_rendu/data/  --outdir=tests_rendu/out
```
