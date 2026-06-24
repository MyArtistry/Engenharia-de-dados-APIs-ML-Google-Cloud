# Engenharia de Dados utilizando APIs de Machine Learning na Google Cloud  
  
# Dataflow job  
## Criei e executei um job no Dataflow
1. Comecei criando o dataset com a tabela no BigQuery.
2. Criei o bucket no Cloud Storage.
3. Acessei o Dataflow e submeti o Job por linha de comando. Disparei a pipeline diretamente pelo Cloud Shell usando a CLI da gcloud. Invoquei o template atualizado de conversão de texto para BigQuery, passando todos os parâmetros obrigatórios em um comando de linha única:

gcloud dataflow jobs run gsp323-dataflow-job \
    gcloud dataflow jobs run gsp323-dataflow-job \
  --gcs-location gs://dataflow-templates-us-east1/latest/GCS_Text_to_BigQuery \
  --region us-east1 \
  --worker-machine-type e2-standard-2 \
