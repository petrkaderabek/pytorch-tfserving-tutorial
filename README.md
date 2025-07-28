# PyTorch-RaggedTensor-TFServing Tutorial

Tensorflow Serving is used to provide an API providing priorities of a particular set of offers for a particular customer in real time. The priorities come from a PyTorch model, which consumes customer ID and returns vector of priorities of all available offers. This model has to be convertes to Tensorflow SavedModel format for TF Serving to be able to use it. Additionally, TF Ragged Tensors are used: The API is queried for a particular set of offers but the PyTorch model returns all offers.

## Model

A dummy SavedModel model is produced by a Jupyter notebook `notebooks/create_savedmodel.ipynb`.

Jupyter is run by `poetry run jupyter notebook`.

## Docker

Run the containers by `docker-compose up -d`.

TensorFlow Serving will be available at `localhost:8501` (REST API) and Prometheus at `localhost:9090`.

Test
* TF Serving at http://localhost:8501/v1/models/test_model
* Prometheus at http://localhost:9090 

```
curl -X POST http://localhost:8501/v1/models/test_model:predict \
-H "Content-Type: application/json" \
-d '{"instances": [[11, 22, 666]]}'
```
