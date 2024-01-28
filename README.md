# UMAP24

## Requirements
Needed libraries:
- torch
- pandas
- pykeen
- SPARQLWrapper
- wikipedia2vec
- tqdm

## Usage
You can find four scripts in this repository, all of them have tunable parameters
that should be changed by editing the relative code section in the file.

- **data_to_wikiname.py**: This script is used to convert a list of entities,
contained in a tsv file with two columns (id, url), where url is the dbpedia
url, to the entity Wikipedia name. In some cases the Wikipedia PageID extracted
from dbpedia is faulty, so it should be corrected manually by following the
prompt instructions.
- **wikiname_to_emb.py**: The output of the previous script should be passed as
input of this script together with a training file, this one only if you want
to include user embeddings. This script outputs a dictionary of (id, embedding)
pairs, which is dumped in the *wiki2vec_embeddings.pkl* file.
- **train_embeddings.py**: Used to learn the graph embeddings, there are many
adjustable parameters. The output of the previus script can be used as pre-trained
embeddings for the model (optional).
- **train_recommender.py**: Script to train the recommender model and generate
the predictions, many training parameters can be tuned. Of these, **embeddings_file**
should be file generated by the previous script.

## Evaluation
The output lists generated by **train_recommender.py** can be evaluated using
**Elliot**. It needs a test file (we provide test_elliot.tsv for the two datasets)
that should be specified in the Elliot config file.
We also provide a sample config file that should be edited and placed in the
`config_files/` Elliot folder, after that Elliot can be executed through the following
command:
```
python start_experiments.py --config=proxy_rec.yml
```
