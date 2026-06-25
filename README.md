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
hdfs dfs -mkdir -p /data
gsutil cp gs://spls/gsp323/data.txt .
hdfs dfs -put data.txt /data.txt

2. Enviei o Job: No console do Dataproc, preenchi os campos com a classe org.apache.spark.examples.SparkPageRank.  
O jar file:///usr/lib/spark/examples/jars/spark-examples.jar e passei o argumento correto como /data.txt.
  
  
 #  API Cloud Speech-to-Text  
 ## Criei a requisição v1:  
 1. No Cloud Shell, criei o arquivo request.json especificando a API moderna:
    {
  "config": { "encoding": "FLAC", "languageCode": "en-US" },
  "audio": { "uri": "gs://spls/gsp323/task3.flac" }
}  

2. Chamei a API via REST: Usei o comando curl para enviar a requisição autenticada, salvando o retorno diretamente:
curl -s -X POST -H "Authorization: Bearer $(gcloud auth print-access-token)" -H "Content-Type: application/json" --data-binary @request.json "[https://speech.googleapis.com/v1/speech:recognize](https://speech.googleapis.com/v1/speech:recognize)" > result.json  

3. Fiz o upload: Enviei o arquivo para o bucket de destino forçando o formato correto com o comando gsutil -h "Content-Type: application/json" cp result.json gs://[CLOUD_SPEECH_LOCATION].  
  
  <img width="1503" height="680" alt="task3final" src="https://github.com/user-attachments/assets/14262190-9cfa-4ad7-8d00-c6510a8378a3" />

  
# API Cloud Natural Language  
## Estruturei o JSON: Criei o arquivo nl_request.json contendo o texto sobre Odin dentro da estrutura padrão da API:


5. Configurei a infraestrutura: Criei o cluster usando a série E2 (e2-standard-2 para master e para os 2 workers), desmarquei a opção de apenas IP interno e aguardei a execução finalizar.
