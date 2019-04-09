---
title: Use o sparklyr do RStudio
titleSuffix: SQL Server big data clusters
description: Conecte-se ao cluster de big data usando sparklyr do RStudio.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 04/08/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 148e4942babafb35af2efe33eb427f9462f0a47e
ms.sourcegitcommit: 2e7686443a61b1a2cf4ca47d9ab1010b9e9b5188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59291576"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>Usar sparklyr no cluster de big data do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr fornece uma interface de R para Apache Spark. Sparklyr é uma maneira popular dos desenvolvedores do R usar o Spark. Este artigo descreve como usar o sparklyr em um cluster de big data de 2019 do SQL Server (versão prévia) usando o RStudio.

## <a name="prerequisites"></a>Prerequisites

- [Implantar um cluster de big data do SQL Server 2019](quickstart-big-data-cluster-deploy.md).

### <a name="install-rstudio-desktop"></a>Instalar o RStudio Desktop

Instalar e configurar **RStudio Desktop** com as seguintes etapas:

1. Se você estiver executando em um cliente Windows, [baixar e instalar o R 3.4.4](https://cran.rstudio.com/bin/windows/base/old/3.4.4).

1. [Baixar e instalar o RStudio Desktop](https://www.rstudio.com/products/rstudio/download/).

1. Após a conclusão da instalação, execute os comandos a seguir dentro da área de trabalho do RStudio para instalar os pacotes necessários:

   ```RStudio Desktop install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01") install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01") install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## Connect to Spark in a big data cluster

You can use sparklyr to connect from a client to the big data cluster using Livy and the HDFS/Spark gateway. 

In RStudio, create an R script and connect to Spark as in the following example:

> [!TIP]
> For the `<USERNAME>` and `<PASSWORD>` values, use the username (such as root) and password you set during the big data cluster deployment. For the `<IP>` and `<PORT>` values, see the documentation on the [HDFS/Spark gateway](connect-to-big-data-cluster.md#hdfs).

```r
library(sparklyr)
library(dplyr)
library(DBI)

#Specify the Knox username and password
config <- livy_config(user = "<username>", password = "<password>")

httr::set_config(httr::config(ssl_verifypeer = 0L, ssl_verifyhost = 0L))

sc <- spark_connect(master = "https://<IP>:<PORT>/gateway/default/livy/v1",
                    method = "livy",
                    config = config)
```

## <a name="run-sparklyr-queries"></a>Executar consultas de sparklyr

Depois de conectar-se ao Spark, você pode executar o sparklyr. O exemplo a seguir executa uma consulta no conjunto de dados íris usando sparklyr:

```r
iris_tbl <- copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="distributed-r-computations"></a>Cálculos R distribuídos

Um recurso de sparklyr é a capacidade [distribuir cálculos R](https://spark.rstudio.com/guides/distributed-r/) com [spark_apply](https://spark.rstudio.com/reference/spark_apply/).

Como os clusters de big data usam conexões de Livy, você deve definir `packages = FALSE` na chamada para **spark_apply**. Para obter mais informações, consulte o [seção Livy](https://spark.rstudio.com/guides/distributed-r/#livy) da documentação sparklyr em cálculos R distribuídos. Com essa configuração, você só pode usar os pacotes de R que já estão instalados no seu cluster Spark no código R passado para **spark_apply**. O exemplo a seguir demonstra essa funcionalidade:

```r
iris_tbl %>% spark_apply(function(e) nrow(e), names = "nrow", group_by = "Species", packages = FALSE)
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de big data, consulte [quais são os clusters do SQL Server 2019 grandes dados](big-data-cluster-overview.md).