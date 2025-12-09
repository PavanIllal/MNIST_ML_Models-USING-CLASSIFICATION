<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>MNIST ML Models — README</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial; line-height: 1.6; color: #111; background:#f7f9fc; padding: 24px; }
    .container { max-width: 900px; margin: 0 auto; background: #fff; border-radius: 8px; box-shadow: 0 6px 20px rgba(13,38,76,0.06); padding: 28px; }
    h1 { margin-top: 0; color: #0b57a4; letter-spacing: -0.5px; }
    h2 { color: #0b57a4; font-size: 1.05rem; }
    pre { background:#0f1720; color:#d1f0ff; padding:12px; border-radius:6px; overflow:auto; }
    code { background:#eef6ff; padding:2px 6px; border-radius:4px; font-family: monospace; }
    .badge { display:inline-block; margin-right:8px; padding:4px 8px; background:#e8f2ff; color:#0b57a4; border-radius:6px; font-weight:600; font-size:0.9rem; }
    ul { margin-top:0; }
    .footer { font-size:0.9rem; color:#555; margin-top:28px; border-top:1px solid #eee; padding-top:16px; }
    .image { max-width:100%; border-radius:6px; border:1px solid #eee; margin:12px 0; }
    .right { float:right; margin-left:12px; max-width:240px; }
    .note { background:#fff7dd; border-left:4px solid #ffd54d; padding:10px 12px; border-radius:6px; }
  </style>
</head>
<body>
  <div class="container">
    <h1>MNIST Classification Using Machine Learning Models</h1>

    <p><strong>Author:</strong> Pavan Illal</p>

    <!-- If you want to show the banner, add the image file to your repo and update the path below -->
    <!-- Example: <img src="assets/banner.png" alt="MNIST Project" class="image"> -->
    <img src="assets/mnist_banner.png" alt="MNIST project banner" class="right image" />

    <p>
      This repository demonstrates an end-to-end machine learning workflow on the <strong>MNIST</strong> dataset (handwritten digit recognition).
      Multiple classification models are implemented, compared and evaluated using metrics such as accuracy, confusion matrix, classification report,
      ROC curves and AUC (macro-average). The best-performing model is then tuned using <code>GridSearchCV</code> and saved for later use.
    </p>

    <h2>Project Highlights</h2>
    <ul>
      <li>Models implemented: <strong>Logistic Regression, KNN, SVM, Decision Tree, Random Forest, Gradient Boosting, XGBoost, Naive Bayes</strong></li>
      <li>Evaluation: <strong>Accuracy, Confusion Matrix, Precision/Recall/F1</strong> and <strong>ROC–AUC (one-vs-rest, macro-average)</strong></li>
      <li>Hyperparameter tuning: <code>GridSearchCV</code> for the chosen best model</li>
      <li>Model persistence: Save the final model using <code>pickle</code></li>
    </ul>

    <h2>Dataset</h2>
    <p>
      Dataset used: <strong>MNIST in CSV</strong> (Kaggle). If you don't include the full dataset in the repo, provide a link or instructions to download it:
    </p>
    <ul>
      <li>Download from Kaggle: <code>https://www.kaggle.com/datasets/oddrationale/mnist-in-csv</code></li>
      <li>Place the file(s) in the repo root or a <code>data/</code> folder (example names used in code: <code>mnist_train.csv</code>, <code>mnist_test.csv</code>).</li>
    </ul>

    <h2>Quick Setup (Local)</h2>
    <p>Run these commands in your terminal (assumes you have Python & pip installed):</p>
    <pre>python -m venv venv
source venv/bin/activate   # macOS / Linux
venv\Scripts\activate      # Windows

pip install -r requirements.txt</pre>

    <p>If you don't have <code>requirements.txt</code>, install minimal packages:</p>
    <pre>pip install numpy pandas scikit-learn matplotlib xgboost</pre>

    <h2>How to run</h2>
    <ol>
      <li>Open the notebook in Google Colab: <code>MNIST_Project.ipynb</code> (recommended) or run the Python script <code>mnist_prediction.py</code> locally.</li>
      <li>Make sure dataset CSV(s) are available in the working directory or update the path in the script/notebook.</li>
      <li>Run the cells (Colab) or run the script:
        <pre>python mnist_prediction.py</pre>
      </li>
      <li>Outputs will include model accuracies, confusion matrices, ROC curves and AUC scores. The chosen best model will be tuned with GridSearchCV and saved.</li>
    </ol>

    <h2>Files in this repository</h2>
    <ul>
      <li><code>MNIST_Project.ipynb</code> — Google Colab notebook with step-by-step code and results.</li>
      <li><code>mnist_prediction.py</code> — Standalone python script (same pipeline as notebook).</li>
      <li><code>requirements.txt</code> — Python package list (use <code>pip install -r requirements.txt</code>).</li>
      <li><code>data/</code> — (recommended) folder for dataset CSV files (not included if dataset is large).</li>
      <li><code>assets/</code> — images (banner, plots) used in README or docs.</li>
      <li><code>best_mnist_model.pkl</code> — (optional) serialized final model.</li>
    </ul>

    <h2>Evaluation & Outputs</h2>
    <p>
      Typical outputs in the notebook include:
    </p>
    <ul>
      <li>Accuracy, confusion matrix and classification report for each model</li>
      <li>ROC curve plot (one-vs-rest) and macro-average AUC values</li>
      <li>GridSearchCV results (best hyperparameters and CV score)</li>
      <li>Saved model using <code>pickle</code> for future inference</li>
    </ul>

    <h2>Notes & Tips</h2>
    <div class="note">
      <strong>Important:</strong> Datasets can be large — avoid committing big CSVs to your repo. Instead keep a small sample or include download instructions in <code>README</code>.
    </div>

    <h2>License</h2>
    <p>MIT License — see <code>LICENSE</code> (or change license as desired).</p>

    <h2>Contact / Credits</h2>
    <p>
      <strong>Author:</strong> Pavan Illal<br />
      <strong>GitHub:</strong> <a href="https://github.com/PavanIllal">https://github.com/PavanIllal</a><br />
      <strong>Email:</strong> add-your-email@example.com (replace with your email)
    </p>

    <div class="footer">
      Last updated: <script>document.write(new Date().toLocaleDateString());</script>
      <br />
      If you want a <code>README.md</code> (Markdown) or a custom visual banner image included in the repo, tell me and I will generate them.
    </div>
  </div>
</body>
</html>
