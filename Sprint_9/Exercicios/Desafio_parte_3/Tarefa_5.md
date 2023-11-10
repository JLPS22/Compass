# Tarefa 5: Desafio Parte 3 - Processamento da Refined
Criar processamento que lê os dados existentes na Trusted, processá-los e inseri-los na Refined.

### Código do Job:
```
import sys
from awsglue.transforms import *
from awsglue.utils import getResolvedOptions
from pyspark.context import SparkContext
from awsglue.context import GlueContext
from awsglue.job import Job

## @params: [JOB_NAME]
args = getResolvedOptions(sys.argv, ['JOB_NAME','S3_INPUT_PATH','S3_TARGET_PATH'])

sc = SparkContext()
glueContext = GlueContext(sc)
spark = glueContext.spark_session
job = Job(glueContext)
job.init(args['JOB_NAME'], args)

source_file = args['S3_INPUT_PATH']
target_path = args['S3_TARGET_PATH']

df = glueContext.create_dynamic_frame.from_options(
    "s3",
    {
        "paths": [
            source_file
        ]
    },
    "parquet",
)

valNull = Filter.apply(frame=df, f=lambda x: x['paisProduzido'] != 'NULL')

glueContext.write_dynamic_frame.from_options(
    frame = valNull,
    connection_type = "s3",
    connection_options = {"path": target_path},
    format = "parquet")

job.commit()
```