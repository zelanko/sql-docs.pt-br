---
title: Conexão de loopback para SQL Server de um script Python ou R
description: Saiba como usar uma conexão de loopback para se conectar novamente ao SQL Server sobre ODBC para ler ou gravar dados de um script Python ou R executado em sp_execute_external_script. Você pode usar isso quando não for possível usar os argumentos InputDataSet e OutputDataSet de sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/21/2019
ms.topic: conceptual
author: Aniruddh25
ms.author: anmunde
ms.reviewer: dphansen
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 62b4ce483df2d38e5e2549d054c02b6c797837f3
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69657483"
---
# <a name="loopback-connection-to-sql-server-from-a-python-or-r-script"></a>Conexão de loopback para SQL Server de um script Python ou R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Saiba como usar uma conexão de loopback para se conectar novamente ao SQL Server sobre [ODBC](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md) para ler ou gravar dados de um script Python ou R executado `sp_execute_external_script`do. Você pode usar isso ao usar os argumentos **InputDataSet** e **OutputDataSet** do `sp_execute_external_script` não é possível.

## <a name="connection-string"></a>Cadeia de conexão

Para fazer uma conexão de auto-retorno, você precisa usar uma cadeia de conexão correta. Os argumentos obrigatórios comuns são o nome do [driver ODBC](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md), o endereço do servidor e o nome do banco de dados.

### <a name="connection-string-on-windows"></a>Cadeia de conexão no Windows

Para autenticação no SQL Server no Windows, o script Python ou R pode usar o atributo de cadeia de conexão **Trusted_Connection** para autenticar como o mesmo usuário que executou o sp_execute_external_script.

Aqui está um exemplo da cadeia de conexão de auto-retorno no Windows:

``` 
"Driver=SQL Server;Server=.;Database=nameOfDatabase;Trusted_Connection=Yes;"
```

### <a name="connection-string-on-linux"></a>Cadeia de conexão no Linux

Para autenticação no SQL Server em Linux, o script Python ou R precisa usar os atributos **ClientCertificate** e **CLIENTKEY vazio** do driver ODBC para autenticar como o mesmo usuário executado `sp_execute_external_script`. Isso requer o uso da versão [mais recente do driver ODBC](../../connect/odbc/download-odbc-driver-for-sql-server.md) 17.4.1.1.

Aqui está um exemplo da cadeia de conexão de auto-retorno no Linux:

```
"Driver=ODBC Driver 17 for SQL Server;Server=fe80::8012:3df5:0:5db1%eth0;Database=nameOfDatabase;ClientCertificate=file:/var/opt/mssql-extensibility/data/baeaac72-60b3-4fae-acfd-c50eff5d34a2/sqlsatellitecert.pem;ClientKey=file:/var/opt/mssql-extensibility/data/baeaac72-60b3-4fae-acfd-c50eff5d34a2/sqlsatellitekey.pem;TrustServerCertificate=Yes;Trusted_Connection=no;Encrypt=Yes"
```

O endereço do servidor, o local do arquivo de certificado do cliente e o local do arquivo `sp_execute_external_script` de chave do cliente são exclusivos para cada e podem ser obtidos pelo uso da API **rx_get_sql_loopback_connection_string ()** para Python ou  **rxGetSqlLoopbackConnectionString ()** para R.

Para obter mais informações sobre os atributos da cadeia de conexão, consulte o [DSN e as palavras-chave da cadeia de conexão e os atributos](https://docs.microsoft.com/sql/connect/odbc/dsn-connection-string-attribute?view=sql-server-linux-ver15#new-connection-string-keywords-and-connection-attributes) para Microsoft ODBC driver for SQL Server.

## <a name="generate-connection-string-with-revoscalepy-for-python"></a>Gerar cadeia de conexão com revoscalepy para Python

Você pode usar a API **rx_get_sql_loopback_connection_string ()** em [revoscalepy](../python/ref-py-revoscalepy.md) para gerar uma cadeia de conexão correta para uma conexão de auto-retorno em um script Python.

Ele aceita os seguintes argumentos:

| Argumento | Descrição |
|-|-|
| name_of_database | Nome do banco de dados para o qual a conexão deve ser feita |
| odbc_driver | Nome do driver ODBC |

### <a name="examples"></a>Exemplos

Exemplo para SQL Server no Windows:

```sql
EXECUTE sp_execute_external_script
@language = N'Python',
@script = N'
from revoscalepy import rx_get_sql_loopback_connection_string, RxSqlServerData, rx_data_step
loopback_connection_string = rx_get_sql_loopback_connection_string(odbc_driver="SQL Server", name_of_database="DBName")
print("Connection String:{0}".format(loopback_connection_string))
data_set = RxSqlServerData(sql_query = "select col1, col2 from tableName",
                           connection_string = loopback_connection_string)
OutputDataSet = rx_data_step(data_set)
'
WITH RESULT SETS ((col1 int, col2 int))
GO
```

Exemplo para SQL Server em Linux:

```sql
EXECUTE sp_execute_external_script
@language = N'Python',
@script = N'
from revoscalepy import rx_get_sql_loopback_connection_string, RxSqlServerData, rx_data_step
loopback_connection_string = rx_get_sql_loopback_connection_string(odbc_driver="ODBC Driver 17 for SQL Server",
                                                                   name_of_database="DBName")
print("Loopback Connection String:{0}".format(loopback_connection_string))
data_set = RxSqlServerData(sql_query = "select col1, col2 from tableName",
                           connection_string = loopback_connection_string)
OutputDataSet = rx_data_step(data_set)
'
WITH RESULT SETS ((col1 int, col2 int))
GO
```

## <a name="generate-connection-string-with-revoscaler-for-r"></a>Gerar cadeia de conexão com RevoScaleR para R

Você pode usar a API **rxGetSqlLoopbackConnectionString ()** em [RevoScaleR](../r/ref-r-revoscaler.md) para gerar uma cadeia de conexão correta para uma conexão de auto-retorno em um script R.

Ele aceita os seguintes argumentos:

| Argumento | Descrição |
|-|-|
| nameOfDatabase | Nome do banco de dados para o qual a conexão deve ser feita |
| odbcDriver | Nome do driver ODBC |

### <a name="examples"></a>Exemplos

Exemplo para SQL Server no Windows:

```sql
EXECUTE sp_execute_external_script
@language = N'R',
@script = N'
    loopbackConnectionString <- rxGetSqlLoopbackConnectionString(nameOfDatabase="DBName", odbcDriver ="SQL Server")
    print(paste("Connection String:", loopbackConnectionString))
    dataSet <- RxSqlServerData(sqlQuery = "select col1, col2 from tableName",
                               connectionString = loopbackConnectionString)
    OutputDataSet <- rxDataStep(dataSet)
'
WITH RESULT SETS ((col1 int, col2 int))
GO
```

Exemplo para SQL Server em Linux:

```sql
EXECUTE sp_execute_external_script
@language = N'R',
@script = N'
    loopbackConnectionString <-  rxGetSqlLoopbackConnectionString(nameOfDatabase="DBName", 
                                                                  odbcDriver ="ODBC Driver 17 for SQL Server")
    print(paste("Connection String:", loopbackConnectionString))
    dataSet <- RxSqlServerData(sqlQuery = "select col1, col2 from tableName", 
                               connectionString = loopbackConnectionString)
    OutputDataSet <- rxDataStep(dataSet)
'
WITH RESULT SETS ((col1 int, col2 int))
GO
```

## <a name="next-steps"></a>Próximas etapas

+ [Driver ODBC da Microsoft para SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)
+ [revoscalepy](../python/ref-py-revoscalepy.md)
+ [RevoScaleR](../r/ref-r-revoscaler.md)
