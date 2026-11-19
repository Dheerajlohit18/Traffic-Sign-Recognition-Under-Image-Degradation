# Traffic Sign Recognition Under Image Degradation

This [notebook](explaination.ipynb) compares a custom CNN and a fine-tuned MobileNetV3-Small on the 43-class German Traffic Sign Recognition Benchmark (GTSRB). Both models use the same test images under three conditions: clean, Gaussian blur, and reduced brightness. A majority-class predictor provides a baseline.

## Saved test results

| Model | Clean accuracy | Blurred accuracy | Low-light accuracy |
| --- | ---: | ---: | ---: |
| Majority-class baseline | 5.94% | 5.94% | 5.94% |
| Custom CNN | 42.08% | 18.61% | 27.02% |
| MobileNetV3-Small | 94.81% | 55.63% | 88.06% |

These figures come from the saved notebook run. Gaussian blur caused the largest accuracy drop for both trained models. The notebook also reports macro F1, macro recall, and a per-class report and confusion matrix for MobileNetV3-Small on clean images.

## Run on Kaggle

1. Open [explaination.ipynb](explaination.ipynb) in Kaggle and attach the GTSRB image dataset.
2. Set `BASE_DIR` in the first code cell. By default, the notebook looks for the images under `train-and-test/Train` and `train-and-test/Test` and the metadata in `csv-files`. Adjust `TRAIN_IMAGE_DIR`, `TEST_IMAGE_DIR`, and `CSV_DIR` for your layout.
3. Run all cells. The first run may need internet access to download the pretrained MobileNetV3-Small weights.

The repository includes `Train.csv`, `Test.csv`, and `Meta.csv`. The image files come from the attached dataset.

## Run locally

```sh
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter notebook
```

On Windows PowerShell, activate the environment with `.venv\Scripts\Activate.ps1`. Open the notebook, set the image and CSV paths to your local dataset, and choose a writable `OUTPUT_DIR`.

The notebook writes the model weights, comparison metrics, training history, class mapping, classification report, and confusion matrix to that output directory. In Kaggle, the default is `/kaggle/working/traffic_sign_results`.

## References

- Stallkamp et al. (2012), [Benchmarking machine learning algorithms for traffic sign recognition](https://doi.org/10.1016/j.neunet.2012.02.016)
- Howard et al. (2019), [Searching for MobileNetV3](https://arxiv.org/abs/1905.02244)
- Hendrycks and Dietterich (2019), [Benchmarking Neural Network Robustness to Common Corruptions and Perturbations](https://arxiv.org/abs/1903.12261)
