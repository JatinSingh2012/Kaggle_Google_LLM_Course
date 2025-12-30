# Loading the 20 Newsgroups Dataset

The Day 2 notebook "Classifying embeddings with Keras" requires the **20 Newsgroups Text Dataset** to work properly. This dataset needs to be downloaded separately and placed in the correct location.

## What is the 20 Newsgroups Dataset?

The [20 Newsgroups Text Dataset](https://scikit-learn.org/stable/datasets/twenty_newsgroups.html) contains 18,000 newsgroup posts across 20 different topics. It's commonly used for text classification and natural language processing tasks.

The dataset is split into:
- **Training set** (`20news-bydate-train/`): Posts from before a specific date
- **Test set** (`20news-bydate-test/`): Posts from after that date

## How to Download the Dataset

### Option 1: Automatic Download via scikit-learn (Recommended)

The easiest way is to let scikit-learn download it automatically on first use:

```python
from sklearn.datasets import fetch_20newsgroups

# This will automatically download the dataset to ~/scikit_learn_data/
train = fetch_20newsgroups(subset='train', remove=('headers', 'footers', 'quotes'))
test = fetch_20newsgroups(subset='test', remove=('headers', 'footers', 'quotes'))
```

### Option 2: Manual Download

If you prefer to download manually or need more control:

1. **Download the dataset directly:**
   ```bash
   cd ~
   mkdir -p scikit_learn_data/20news-bydate
   cd scikit_learn_data/20news-bydate
   
   # Download the dataset from UCI Machine Learning Repository
   wget http://qwone.com/~jason/20Newsgroups/20news-bydate.tar.gz
   
   # Extract the archive
   tar -xzf 20news-bydate.tar.gz
   ```

2. **Or using curl:**
   ```bash
   cd ~/scikit_learn_data
   curl -O http://qwone.com/~jason/20Newsgroups/20news-bydate.tar.gz
   tar -xzf 20news-bydate.tar.gz
   ```

### Option 3: Using Python

```python
import os
import urllib.request
import tarfile

# Create the data directory
data_dir = os.path.expanduser("~/scikit_learn_data")
os.makedirs(data_dir, exist_ok=True)

# Download the dataset
url = "http://qwone.com/~jason/20Newsgroups/20news-bydate.tar.gz"
tar_path = os.path.join(data_dir, "20news-bydate.tar.gz")

print("Downloading dataset...")
urllib.request.urlretrieve(url, tar_path)

# Extract the dataset
print("Extracting dataset...")
with tarfile.open(tar_path, "r:gz") as tar:
    tar.extractall(data_dir)

print("Dataset ready!")
```

## Expected Directory Structure

After downloading, your directory should look like this:

```
~/scikit_learn_data/
├── 20news-bydate-train/
│   ├── alt.atheism/
│   ├── comp.graphics/
│   ├── comp.os.ms-windows.misc/
│   ├── comp.sys.ibm.pc.hardware/
│   ├── comp.sys.mac.hardware/
│   ├── comp.windows.x/
│   ├── misc.forsale/
│   ├── rec.autos/
│   ├── rec.motorcycles/
│   ├── rec.sport.baseball/
│   ├── rec.sport.hockey/
│   ├── sci.crypt/
│   ├── sci.electronics/
│   ├── sci.med/
│   ├── sci.space/
│   ├── soc.religion.christian/
│   ├── talk.atheism/
│   ├── talk.politics.guns/
│   ├── talk.politics.mideast/
│   └── talk.politics.misc/
└── 20news-bydate-test/
    └── [same 20 categories as above]
```

## Verification

To verify the dataset is correctly installed, run this Python code:

```python
import os

train_path = os.path.expanduser("~/scikit_learn_data/20news-bydate-train")
test_path = os.path.expanduser("~/scikit_learn_data/20news-bydate-test")

if os.path.exists(train_path) and os.path.exists(test_path):
    print("✓ Dataset is correctly installed!")
    print(f"Training categories: {len(os.listdir(train_path))}")
    print(f"Test categories: {len(os.listdir(test_path))}")
else:
    print("✗ Dataset not found. Please follow the installation instructions above.")
```

## Using the Dataset in the Notebook

Once installed, the notebook uses it like this:

```python
from sklearn.datasets import load_files
import os

# Load the raw data
train_path = os.path.expanduser("~/scikit_learn_data/20news-bydate-train")
test_path = os.path.expanduser("~/scikit_learn_data/20news-bydate-test")

train = load_files(train_path, encoding='latin1')
test = load_files(test_path, encoding='latin1')
```

## Troubleshooting

### "FileNotFoundError: 20news-bydate-train not found"
- The dataset hasn't been downloaded yet
- Ensure the paths are correct (should be in `~/scikit_learn_data/`)
- Try running Option 1 (automatic download via scikit-learn)

### "Connection timeout when downloading"
- Check your internet connection
- Try Option 3 (Python script) for more reliable downloads
- The dataset is about 18MB compressed

### "Permission denied" errors
- Ensure you have write permissions in your home directory
- Try running with appropriate permissions or use a different local directory

## Dataset Details

- **Total posts**: ~18,000
- **Number of categories**: 20
- **Compressed size**: ~18 MB
- **Uncompressed size**: ~200 MB
- **Format**: Plain text files organized by category
- **License**: Public domain (from USENET archives)

## References

- [scikit-learn 20 Newsgroups Documentation](https://scikit-learn.org/stable/datasets/twenty_newsgroups.html)
- [20 Newsgroups Dataset Homepage](http://qwone.com/~jason/20Newsgroups/)
- [UCI Machine Learning Repository](https://archive.ics.uci.edu/)
