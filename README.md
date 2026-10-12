# Traffic Sign Recognition Under Image Degradation

**Comparing a Custom CNN with MobileNetV3-Small for Robust Traffic Sign Classification**

This repository contains a Jupyter notebook that trains and compares a custom CNN and MobileNetV3-Small on the German Traffic Sign Recognition from kaggle.It evaluates the models on clean images , Gaussian-blurred images, and low-light images.
## Project goals

- Train a custom CNN for 43-class traffic sign classification.
- Fine-tune pretrained MobileNetV3-Small.
- Compare accuracy , macro F1-score and macro recall under three image conditions.
- Inspect class-level results with a classification report and confusion matrix.

## Repository contents

```text
traffic-sign-recognition/
├── README.md
├── requirements.txt
└── traffic_sign_recognition_explained.ipynb
```

The notebook includes explanations in Markdown cells and comments inside the code cells.Results and trained weights are generated when the notebook is run; they are not required to start the project.

## Recommended way to run: Kaggle

The notebook currently uses Kaggle-style dataset paths.Kaggle is the easiest option because the dataset can be attached directly to the notebook.

1. Sign in to Kaggle and create a new notebook.
2. Add the GTSRB dataset containing `Train.csv`, `Test.csv`, `Meta.csv`, and the corresponding train/test image folders.
3. Open or upload `traffic_sign_recognition_explained.ipynb`.
4. In the first code cell, update `BASE_DIR` to the actual dataset directory shown in the Kaggle input panel. The expected structure in the current notebook is:

   ```text
   <BASE_DIR>/
   ├── train-and-test/
   │   ├── Train/
   │   └── Test/
   └── csv-files/
       ├── Train.csv
       ├── Test.csv
       └── Meta.csv
   ```

 If your dataset has a different folder structure , update `TRAIN_IMAGE_DIR`, `TEST_IMAGE_DIR` and `CSV_DIR` in the first cell.

### 1. Download the dataset

Download/access GTSRB from a source whose terms permit your intended use.Extract it locally and make sure the CSV files and image folders are available.

### 2. Set up Python

Python 3.10 or 3.11 is a practical choice for PyTorch compatibility.Create and activate a virtual environment:

**macOS/Linux**
```bash
python3 -m venv .venv
source .venv/bin/activate
```

**Windows (PowerShell)**
```powershell
py -m venv .venv
.venv\Scripts\Activate.ps1
```

### 3. Install packages

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Update dataset paths

The notebook currently has Kaggle paths such as `/kaggle/input/...` and an output path under `/kaggle/working`. For local execution, edit the first code cell and point the paths to your local dataset, for example:

```python
BASE_DIR = Path("data/GTSRB")  # Change this to your extracted dataset folder

TRAIN_IMAGE_DIR = BASE_DIR / "train-and-test" / "Train"
TEST_IMAGE_DIR = BASE_DIR / "train-and-test" / "Test"
CSV_DIR = BASE_DIR / "csv-files"

OUTPUT_DIR = Path("results/traffic_sign_results")
OUTPUT_DIR.mkdir(parents=True, exist_ok=True)
```

These example paths work only if your local folders follow the shown structure.Adjust them to match your actual dataset.

### 5. Start Jupyter

```bash
python -m pip install notebook
jupyter notebook
```

Open `traffic_sign_recognition_explained.ipynb` in the browser and choose **Run → Run All Cells**.You can also use Visual Studio Code with the Jupyter extension.

## What the notebook does

1. Imports libraries and configures the environment.
2. Loads CSV metadata and resolves image paths.
3. Checks class labels and displays sample images.
4. Preprocesses images and creates data loaders.
5. Establishes a majority-class baseline.
6. Builds and trains a custom CNN.
7. Loads pretrained MobileNetV3-Small and fine-tunes its classifier.
8. Evaluates both models on clean, blurred, and low-light images.
9. Reports accuracy, macro F1-score, and macro recall.
10. Produces metric plots, a classification report, and a confusion matrix.
11. Saves model weights and experiment metadata.

## Output files

When the final cell completes , the results folder contains files such as:

- `custom_cnn.pth` — custom CNN weights
- `mobilenetv3_small.pth` — MobileNetV3-Small weights
- `model_comparison.csv` — comparison metrics
- `training_history.json` — loss and accuracy history
- `class_mapping.json` — mapping between model label indices and original class IDs
- `experiment_config.json` — key experiment settings
- `classification_report.csv` — detailed classification report

The exact files depend on which cells complete successfully.In Kaggle, download outputs from the working directory before the session ends.

## Important notes

- The results depend on dataset version , paths , random seeds , training configuration and hardware.Re-run the notebook to reproduce the table rather than assuming old numbers will be identical.
- The pretrained MobileNetV3-Small weights may need to be downloaded on the first run.
- The experiment tests only Gaussian blur and reduced brightness;it does not prove reliability in all real-world driving conditions.
- Do not commit Kaggle API tokens , passwords , private credentials the complete dataset or large model weights unless you have checked licensing and repository-size constraints.
- Only report results that were actually generated by your run.

## Upload to GitHub

### Option A: Upload through the GitHub website

1. Sign in to GitHub and create a **new repository**.A suitable name is `traffic-sign-recognition`.
2. Set the repository to Public or Private as appropriate.
3. On your computer , place these files in one project folder:
   - `README.md`
   - `requirements.txt`
   - `traffic_sign_recognition_explained.ipynb`
4. In the new repository , select **Add file → Upload files**.
5. Drag the three files into the upload area.
6. Add a commit message such as `Add explained traffic sign recognition notebook`.
7. Select **Commit changes**.

### Option B: Upload with Git

Install Git if needed , then open a terminal in the project folder:

```bash
git init
git add README.md requirements.txt traffic_sign_recognition_explained.ipynb
git commit -m "Add explained traffic sign recognition project"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/traffic-sign-recognition.git
git push -u origin main
```

Replace `YOUR-USERNAME` with your GitHub username and use the actual repository URL.If Git says the remote already exists, check it with `git remote -v` rather than adding it again.

### Suggested `.gitignore`

Create a file named `.gitignore` to avoid uploading temporary files , environments, datasets, and large generated outputs:

```gitignore
.venv/
__pycache__/
.ipynb_checkpoints/
data/
*.pth
*.pt
.kaggle/
```

If you intentionally want to version selected trained weights or results, review their size and licensing first,then remove the relevant ignore rule.

## References

1. Stallkamp, J., Schlipsing, M., Salmen, J., & Igel, C. (2012). *Man vs. computer: Benchmarking machine learning algorithms for traffic sign recognition.* Neural Networks, 32, 323–332. https://doi.org/10.1016/j.neunet.2012.02.016
2. Cireșan, D. C., Meier, U., Masci, J., & Schmidhuber, J. (2012). *Multi-column deep neural network for traffic sign classification.* Neural Networks, 32, 333–338. https://doi.org/10.1016/j.neunet.2012.02.023
3. Howard, A., et al. (2019). *Searching for MobileNetV3.* ICCV. https://arxiv.org/abs/1905.02244
4. Hendrycks, D., & Dietterich, T. (2019). *Benchmarking Neural Network Robustness to Common Corruptions and Perturbations.* ICLR. https://arxiv.org/abs/1903.12261
