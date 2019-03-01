---
title: Use o sparklyr do RStudio
titleSuffix: SQL Server 2019 big data clusters
description: Conecte-se ao cluster de Big data usando o sparklyr do RStudio.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 83980f9d08a3894b0fbf7871cf899483e06702c4
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018352"
---
# <a name="use-sparklyr-in-sql-server-2019-big-data-cluster"></a>Usar Sparklyr no cluster de dados do SQL Server de 2019 grande

Sparklyr fornece uma interface de R para Apache Spark. Sparklyr é a maneira preferencial para os desenvolvedores do R usar o Spark. Este artigo descreve como usar o sparklyr em um cluster de big data de 2019 do SQL Server (versão prévia) usando o RStudio.

## <a name="prerequisites"></a>Prerequisites

- [Implantar um cluster de big data do SQL Server 2019](quickstart-big-data-cluster-deploy.md).
- [Instalar o RStudio](https://www.rstudio.com/)

## <a name="connect-to-spark-in-ss19-big-data-cluster"></a>Conectar-se para o spark no cluster SS19 Big Data

No RStudio, criar um RScript e conecte-se para o Spark da seguinte maneira. Cluster do Spark Big data se conecta por meio do Livy, que pode ser alcançado com o [gateway HDFS/Spark](connect-to-big-data-cluster.md#hdfs). Para autenticação, use o nome de usuário e a senha especificados durante a implantação.

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