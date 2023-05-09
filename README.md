# DoCoGen Lite
<a name="lite"/>

The DoCoGen Lite script is a single script version of the DoCoGen generator.
It is a more simple and readable code that does not require PyTorch-Lightning.
This modified DoCoGen code can be used to generate counterfactuals in multiple languages supported by HuggingFace MT5 model

## How to Run the Code - 
1. Clone this repository 
```bash
gh repo clone madhav1412/DoCoGen
```

2. Navigate to the directory
```bash
cd DoCoGen
```
3. Create conda virtual environment
```bash
conda env create -f docogen_lite_env.yml
```
4. Activate the create conda environment
```bash
conda activate docogen_lite_env
```
5. unzip the dataset in the data/ directory
```bash
unzip data/paper_data.zip -d data/
```
6. Run the DoCoGen script
```bash
python docogen_lite.py --dataset_file_path data/reviews.json --output_dir path/to/output_dir --domains_to_control airline dvd electronics kitchen
```


## Arguments

```text
  -h, --help            show this help message and exit
  --dataset_file_path DATASET_FILE_PATH
                        (str) Path to the dataset file (.json). Must include
                        the following fields: "text", "domain"
  --output_dir OUTPUT_DIR
                        (str) Path to the output directory where the following
                        files will be save: (1) preprocessed datasets, (2)
                        masker, (3) trained domain classifier, (4) trained
                        DoCoGen (including the training outputs), (5) domain-
                        counterfactuals.
  --domains_to_control DOMAINS_TO_CONTROL [DOMAINS_TO_CONTROL ...]
                        (list of str) List of domains to control (should be
                        values of the "domain" field).
  --model_name MODEL_NAME
                        (str=t5-base) Name of the T5 model to use for the
                        DoCoGen.
  --classifier_name CLASSIFIER_NAME
                        (str=distilroberta-base) Name of the pre-trained model
                        which will be trained to be a domain classifier. This
                        model is part of the evaluation step of DoCoGen.
  --max_length MAX_LENGTH
                        (int=96) Maximum length of the input and the generated
                        texts.
  --eval_size EVAL_SIZE
                        (int=1024) Size of the evaluation set. Use a small
                        value, since the evaluation step of DoCoGen includes
                        generations -- and it is really slow compared to the
                        training.
  --labeled_size LABELED_SIZE
                        (int=16) Size of the labeled dataset which will be
                        used to generate domain-counterfactuals. Use a small
                        size or use `None` if you are interested in the whole
                        dataset.
  --min_n_occurrences MIN_N_OCCURRENCES
                        (int=10) An n-gram which occurs less than this value
                        will have a masking score of zero.
  --smoothing SMOOTHING [SMOOTHING ...]
                        (list of ints/floats=[1, 5, 7]) The n-th element is
                        the smoothing hyperparameter for an n sized n-gram.
                        These hyperparameters are used to smooth the masking
                        score (higher values give more weight to the uniform
                        prior). In addition, the length of the smoothing list
                        determines the maximum n-gram size.
  --batch_size_classifier BATCH_SIZE_CLASSIFIER
                        (int=64) Batch size for the domain classifier.
  --batch_size_docogen BATCH_SIZE_DOCOGEN
                        (int=32) Batch size for DoCoGen.
  --docogen_epochs DOCOGEN_EPOCHS
                        (int=5) Number of epochs for DoCoGen training.
  --num_beams NUM_BEAMS
                        (int=4) Number of beams for DoCoGen generation.
  --generate_all_orientations GENERATE_ALL_ORIENTATIONS
                        (bool=False) If `True`, all possible orientations will
                        be generated for each example. Otherwise, randomly
                        sample an orientation.
  --print_generated_texts PRINT_GENERATED_TEXTS
                        (bool=True) If `True`, the generated texts will be
                        printed.
  --seed SEED
```
