---
title: Conexão de loopback do SQL
description: Saiba como usar uma conexão de loopback para se conectar novamente ao SQL Server por ODBC a fim de ler ou gravar dados de um script Python ou R executado de sp_execute_external_script. Você poderá usar isso quando não for possível usar os argumentos InputDataSet e OutputDataSet de sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/21/2019
ms.topic: conceptual
author: Aniruddh25
ms.author: anmunde
ms.reviewer: dphansen
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c7fa36db48a7912951f0232136945798caf6f7f7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727593"
---
# <a name="loopback-connection-to-sql-server-from-a-python-or-r-script"></a>Conexão de loopback para o SQL Server de um script Python ou R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Saiba como usar uma conexão de loopback para se conectar novamente ao SQL Server por [ODBC](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md) a fim de ler ou gravar dados de um script Python ou R executado de `sp_execute_external_script`. Você poderá usar isso quando não for possível usar os argumentos **InputDataSet** e **OutputDataSet** de `sp_execute_external_script`.

## <a name="connection-string"></a>Cadeia de conexão

Para fazer uma conexão loopback, você precisa usar uma cadeia de conexão correta. Os argumentos normalmente obrigatórios são o nome do [driver ODBC](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md), o endereço do servidor e o nome do banco de dados.

### <a name="connection-string-on-windows"></a>Cadeia de conexão no Windows

Para autenticação no SQL Server no Windows, o script Python ou R pode usar o atributo de cadeia de conexão **Trusted_Connection** para autenticar como o mesmo usuário que executou o sp_execute_external_script.

Aqui está um exemplo da cadeia de conexão de loopback no Windows:

``` 
"Driver=SQL Server;Server=.;Database=nameOfDatabase;Trusted_Connection=Yes;"
```

### <a name="connection-string-on-linux"></a>Cadeia de conexão no Linux

Para autenticação no SQL Server em Linux, o script Python ou R precisa usar os atributos **ClientCertificate** e **ClientKey** do driver ODBC para autenticar como o mesmo usuário que executou `sp_execute_external_script`. Isso requer o uso do [driver ODBC mais recente](../../connect/odbc/download-odbc-driver-for-sql-server.md), versão 17.4.1.1.

Aqui está um exemplo da cadeia de conexão de loopback em Linux:

```
"Driver=ODBC Driver 17 for SQL Server;Server=fe80::8012:3df5:0:5db1%eth0;Database=nameOfDatabase;ClientCertificate=file:/var/opt/mssql-extensibility/data/baeaac72-60b3-4fae-acfd-c50eff5d34a2/sqlsatellitecert.pem;ClientKey=file:/var/opt/mssql-extensibility/data/baeaac72-60b3-4fae-acfd-c50eff5d34a2/sqlsatellitekey.pem;TrustServerCertificate=Yes;Trusted_Connection=no;Encrypt=Yes"
```

O endereço do servidor, a localização do arquivo de certificado do cliente e a localização do arquivo de chave do cliente são exclusivos para cada `sp_execute_external_script` e podem ser obtidos pelo uso da API **rx_get_sql_loopback_connection_string()** para Python ou **rxGetSqlLoopbackConnectionString()** para R.

Para obter mais informações sobre os atributos da cadeia de conexão, confira os [Atributos e palavras-chave da cadeia de conexão e DSN](https://docs.microsoft.com/sql/connect/odbc/dsn-connection-string-attribute?view=sql-server-linux-ver15#new-connection-string-keywords-and-connection-attributes) para o Microsoft ODBC Driver for SQL Server.

## <a name="generate-connection-string-with-revoscalepy-for-python"></a>Gerar cadeia de conexão com o revoscalepy para Python

Você pode usar a API **rx_get_sql_loopback_connection_string ()** em [revoscalepy](../python/ref-py-revoscalepy.md) para gerar uma cadeia de conexão correta para uma conexão de loopback em um script Python.

Ela aceita os seguintes argumentos:

| Argumento | DESCRIÇÃO |
|-|-|
| name_of_database | Nome do banco de dados para o qual a conexão deve ser feita |
| odbc_driver | O nome do driver ODBC |

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

## <a name="generate-connection-string-with-revoscaler-for-r"></a>Gerar cadeia de conexão com o RevoScaleR para R

Você pode usar a API **rxGetSqlLoopbackConnectionString()** em [RevoScaleR](../r/ref-r-revoscaler.md) para gerar uma cadeia de conexão correta para uma conexão de loopback em um script R.

Ela aceita os seguintes argumentos:

| Argumento | DESCRIÇÃO |
|-|-|
| nameOfDatabase | Nome do banco de dados para o qual a conexão deve ser feita |
| odbcDriver | O nome do driver ODBC |

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

+ [Microsoft ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)
+ [revoscalepy](../python/ref-py-revoscalepy.md)
+ [RevoScaleR](../r/ref-r-revoscaler.md)
