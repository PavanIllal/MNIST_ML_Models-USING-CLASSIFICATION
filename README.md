<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>MNIST_Classification — README</title>
  <style>
    body{font-family:system-ui,-apple-system,Segoe UI,Roboto,'Helvetica Neue',Arial;line-height:1.6;padding:24px;color:#0b1220;background:#f7f8fb}
    header{max-width:900px;margin:0 auto 18px}
    main{max-width:900px;margin:0 auto;background:white;padding:22px;border-radius:12px;box-shadow:0 6px 20px rgba(12,15,30,0.06)}
    h1{margin:0 0 6px;font-size:28px}
    p.lead{color:#374151}
    pre{background:#0b1220;color:#e6eef8;padding:12px;border-radius:8px;overflow:auto}
    code{background:#eef2ff;padding:2px 6px;border-radius:4px}
    section{margin-top:18px}
    ul{margin-left:18px}
    .badge{display:inline-block;padding:6px 10px;border-radius:999px;background:#eef2ff;margin-right:8px;font-size:13px}
    footer{max-width:900px;margin:18px auto;color:#6b7280;font-size:13px}
  </style>
</head>
<body>
  <header>
    <h1>MNIST Classification Pipeline</h1>
    <p class="lead">A simple, modular pipeline to train and evaluate multiple classical ML models on the MNIST-style CSV image dataset (pixel columns + label). This repository includes model training, evaluation (accuracy & classification report), ROC–AUC (one-vs-rest for class `1`), and GridSearchCV hyperparameter tuning.</p>
  </header>

  <main>
    <section>
      <div class="badge">Python</div>
      <div class="badge">scikit-learn</div>
      <div class="badge">pandas</div>
      <div class="badge">matplotlib</div>
    </section>

    <section>
      <h2>Table of contents</h2>
      <ol>
        <li>Overview</li>
        <li>Repository structure</li>
        <li>Requirements</li>
        <li>How to run</li>
        <li>What the script does</li>
        <li>Expected outputs</li>
        <li>Troubleshooting</li>
        <li>Extending the project</li>
        <li>License & Contact</li>
      </ol>
    </section>

    <section>
      <h2>Overview</h2>
      <p>This project demonstrates training multiple classical ML models (Logistic Regression, KNN, SVM, Decision Tree, Random Forest, Naive Bayes, Gradient Boosting) on an MNIST-style CSV file where each row contains a <code>label</code> column and pixel features (e.g. <code>pixel0, pixel1, ...</code>).</p>
    </section>

    <section>
      <h2>Repository structure</h2>
      <pre><code>.
├─ README_MNIST_Classification.html   # (this file)
├─ mnist_classification.py            # main class-based pipeline (MNIST_CLASSIFICATION)
├─ requirements.txt                   # recommended packages
└─ data/
   └─ mnist_test.csv                   # example CSV (not included)
</code></pre>
    </section>

    <section>
      <h2>Requirements</h2>
      <p>Recommended Python packages (tested with Python 3.8+):</p>
      <pre><code>pip install numpy pandas matplotlib scikit-learn</code></pre>
      <p>Optional: create a <code>requirements.txt</code> with:</p>
      <pre><code>numpy
pandas
matplotlib
scikit-learn</code></pre>
    </section>

    <section>
      <h2>How to run</h2>
      <p>Place your MNIST-style CSV file (with a <code>label</code> column and pixel feature columns) somewhere accessible and update the <code>dataset_path</code> in the script or pass the path when instantiating the class.</p>

      <p>Example — run as a script:</p>
      <pre><code>python mnist_classification.py
# or if your script file name differs, update accordingly</code></pre>

      <p>If you prefer to run from an interactive notebook:</p>
      <pre><code>from mnist_classification import MNIST_CLASSIFICATION
obj = MNIST_CLASSIFICATION('/path/to/mnist_test.csv')
obj.execute_models()
obj.roc_auc_stage2()
obj.stage3_gridsearch()</code></pre>

      <p><strong>Important:</strong> Update the dataset path inside the <code>if __name__ == '__main__'</code> block before running, or pass a correct path when creating the object.</p>
    </section>

    <section>
      <h2>What the script does (high level)</h2>
      <ul>
        <li>Reads CSV into a Pandas DataFrame and splits <code>X</code> and <code>y</code>.</li>
        <li>Performs a train/test split (80/20).</li>
        <li>Stage 1: Trains multiple classification models and prints accuracy, confusion matrix, and classification report for each.</li>
        <li>Stage 2: Calculates ROC & AUC for class <code>1</code> vs rest (one-vs-rest); plots ROC curves and reports AUC scores for each model.</li>
        <li>Stage 3: Picks best model by AUC and runs GridSearchCV to tune hyperparameters (skips tuning for Naive Bayes).</li>
      </ul>
    </section>

    <section>
      <h2>Expected outputs</h2>
      <ul>
        <li>Console logs with accuracy, confusion matrix and classification reports for each model.</li>
        <li>ROC plot (shown with <code>matplotlib</code>) and printed AUC scores.</li>
        <li>If GridSearch runs, best parameters and the final tuned estimator will be printed.</li>
      </ul>
    </section>

    <section>
      <h2>Troubleshooting & notes</h2>
      <ul>
        <li><strong>CSV format:</strong> Ensure the CSV has a header row and a column named exactly <code>label</code>.</li>
        <li><strong>Multiclass AUC:</strong> The ROC stage uses a one-vs-rest AUC for class <code>1</code>. For a general multiclass AUC, consider <code>sklearn.metrics.roc_auc_score</code> with <code>multi_class='ovr'</code> or compute per-class AUCs.</li>
        <li><strong>predict_proba availability:</strong> Some models (e.g. SVC) require <code>probability=True</code> to use <code>predict_proba</code>. The script already sets this for SVC used in this repo.</li>
        <li><strong>Large dataset / speed:</strong> GridSearchCV with many parameter combinations can be slow — reduce the grid or use randomized search for faster tuning.</li>
        <li><strong>Common errors:</strong> If you see <code>KeyError: 'label'</code>, check the CSV column names. If you see memory errors, try using a smaller sample or increase system memory.</li>
      </ul>
    </section>

    <section>
      <h2>Ideas to extend</h2>
      <ul>
        <li>Use cross-validation to compute stable mean & std of accuracy.</li>
        <li>Implement scale/normalize steps (StandardScaler) inside a Pipeline.</li>
        <li>Try dimensionality reduction (PCA) for speed and visualization.</li>
        <li>Add model persisting with <code>joblib</code> or <code>pickle</code>.</li>
        <li>Replace manual grid search with <code>RandomizedSearchCV</code> for larger search spaces.</li>
      </ul>
    </section>

    <section>
      <h2>License</h2>
      <p>This repository is released under the MIT License — feel free to reuse and adapt (add a LICENSE file to the repo if you want to make it explicit).</p>
    </section>

    <section>
      <h2>Contact</h2>
      <p>Created by Pavan. Open an issue or pull request in the repository for questions or improvements.</p>
    </section>
  </main>

  <footer>
    <p>Generated README for the MNIST Classification pipeline. Update contents as you add files or change the pipeline.</p>
  </footer>
</body>
</html>
