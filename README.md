# Engenharia de Dados utilizando APIs de Machine Learning na Google Cloud  
  
# Dataflow job  
## Criei e executei um job no Dataflow
1. Comecei criando o dataset com a tabela no BigQuery.
2. Criei o bucket no Cloud Storage.
3. Acessei o Dataflow e submeti o Job por linha de comando. Disparei a pipeline diretamente pelo Cloud Shell usando a CLI da gcloud. Invoquei o template atualizado de conversão de texto para BigQuery, passando todos os parâmetros obrigatórios em um comando de linha única:  
   ```gcloud dataflow jobs run gsp323-dataflow-job --gcs-location gs://dataflow-templates-us-east1/latest/GCS_Text_to_BigQuery --region us-east1 --worker-machine-type e2-standard-2 --staging-location gs://qwiklabs-gcp-03-f1c54c1a8105-marking/temp --parameters javascriptTextTransformGcsPath=gs://spls/gsp323/lab.js,JSONPath=gs://spls/gsp323/lab.schema,javascriptTextTransformFunctionName=transform,outputTable=qwiklabs-gcp-03-f1c54c1a8105:lab_778.customers_460,inputFilePattern=gs://spls/gsp323/lab.csv,bigQueryLoadingTemporaryDirectory=gs://qwiklabs-gcp-03-f1c54c1a8105-marking/bigquery_temp```

# Job no Managed Service for Spark (Dataproc)

## Preparei o ambiente HDFS: 
1. Acessei o nó master via SSH, criei a pasta de destino e depois copiei o arquivo do Cloud Storage para o sistema HDFS do cluster executando:  
  ```hdfs dfs -mkdir -p /data
gsutil cp gs://spls/gsp323/data.txt .
hdfs dfs -put data.txt /data.txt```

2. Enviei o Job: No console do Dataproc, preenchi os campos com a classe org.apache.spark.examples.SparkPageRank.  
  ```O jar file:///usr/lib/spark/examples/jars/spark-examples.jar e passei o argumento correto como /data.txt.```
  
3. Configurei a infraestrutura: Criei o cluster usando a série E2 (e2-standard-2 para master e para os 2 workers), desmarquei a opção de apenas IP interno e aguardei a execução finalizar.
