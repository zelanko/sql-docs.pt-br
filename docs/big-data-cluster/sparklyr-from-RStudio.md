---
title: Use o sparklyr do RStudio
titleSuffix: SQL Server big data clusters
description: Conecte-se ao cluster de big data usando sparklyr do RStudio.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 30b8ddccd01c0e8d9a4eac34f2f504b0d8971af6
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860187"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>Usar Sparklyr no cluster de big data do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr fornece uma interface de R para Apache Spark. Sparklyr é a maneira preferencial para os desenvolvedores do R usar o Spark. Este artigo descreve como usar o sparklyr em um cluster de big data de 2019 do SQL Server (versão prévia) usando o RStudio.

## <a name="prerequisites"></a>Prerequisites

- [Implantar um cluster de big data do SQL Server 2019](quickstart-big-data-cluster-deploy.md).
- [Instalar o RStudio](https://www.rstudio.com/)

## <a name="connect-to-spark-in-ss19-big-data-cluster"></a>Conectar-se para o spark no cluster SS19 Big Data

No RStudio, criar um RScript e conecte-se para o Spark da seguinte maneira. Cluster de big data do Spark conecta-se por meio do Livy, que pode ser alcançado com o [gateway HDFS/Spark](connect-to-big-data-cluster.md#hdfs). Para autenticação, use o nome de usuário e a senha especificados durante a implantação.

```r
library(sparklyr)
library(dplyr)
library(DBI)

#Specify the Knox username and password
config <- livy_config(user = "***root***", password = "****")

httr::set_config(httr::config(ssl_verifypeer = 0L))

sc <- spark_connect(master = "https://<IP>:<PORT>/gateway/default/livy/v1",
                    method = "livy",
                    config = config)
```

## <a name="run-sparklyr-queries"></a>Executar consultas de sparklyr

Depois de conectar-se ao Spark, você pode executar o sparklyr. O exemplo a seguir executa uma consulta no conjunto de dados íris usando sparklyr:

``` r
copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de big data, consulte [quais são os clusters do SQL Server 2019 big data?](big-data-cluster-overview.md).