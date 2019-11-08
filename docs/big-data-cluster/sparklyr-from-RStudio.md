---
title: Usar o Sparklyr do RStudio
titleSuffix: SQL Server big data clusters
description: Conecte-se ao cluster de Big Data usando o sparklyr do RStudio.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 375993e4fd9506c129e4f98d9ad2193472e03edb
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531622"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>Usar o sparklyr em clusters de Big Data do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O Sparklyr fornece uma interface R para o Apache Spark. O Sparklyr é uma maneira popular de os desenvolvedores de R usarem o Spark. Este artigo descreve como usar o sparklyr em um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] usando o RStudio.

## <a name="prerequisites"></a>Prerequisites

- [Implantar um cluster de Big Data do SQL Server 2019](quickstart-big-data-cluster-deploy.md).

### <a name="install-rstudio-desktop"></a>Instalar o RStudio Desktop

Instale e configure o **RStudio Desktop** com as seguintes etapas:

1. Se você estiver executando em um cliente Windows, [baixe e instale o R 3.4.4](https://cran.rstudio.com/bin/windows/base/old/3.4.4).

1. [Baixe e instale o RStudio Desktop](https://www.rstudio.com/products/rstudio/download/).

1. Após a conclusão da instalação, execute os seguintes comandos dentro do RStudio Desktop para instalar os pacotes necessários:

   ```RStudioDesktop
   install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## <a name="connect-to-spark-in-a-big-data-cluster"></a>Conectar-se ao Spark em um cluster de Big Data

Você pode usar o sparklyr para conectar-se de um cliente ao cluster de Big Data usando o Livy e o gateway do HDFS/Spark. 

No RStudio, crie um script do R e conecte-se ao Spark como neste exemplo:

> [!TIP]
> Para os valores `<AZDATA_USERNAME>` e `<AZDATA_PASSWORD>`, use o nome de usuário (como raiz) e a senha definidos durante a implantação do cluster de Big Data. Para obter os valores de `<IP>` e `<PORT>`, confira a documentação sobre [conectar-se a um de cluster de Big Data](connect-to-big-data-cluster.md).

```r
library(sparklyr)
library(dplyr)
library(DBI)

#Specify the Knox username and password
config <- livy_config(user = "<AZDATA_USERNAME>", password = "<AZDATA_PASSWORD>")

httr::set_config(httr::config(ssl_verifypeer = 0L, ssl_verifyhost = 0L))

sc <- spark_connect(master = "https://<IP>:<PORT>/gateway/default/livy/v1",
                    method = "livy",
                    config = config)
```

## <a name="run-sparklyr-queries"></a>Executar consultas do sparklyr

Depois de se conectar ao Spark, você pode executar o sparklyr. O exemplo a seguir executa uma consulta no conjunto de dados Iris usando sparklyr:

```r
iris_tbl <- copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="distributed-r-computations"></a>Computações do R distribuídas

Um recurso do sparklyr é a capacidade de [distribuir computações do R](https://spark.rstudio.com/guides/distributed-r/) com [spark_apply](https://spark.rstudio.com/reference/spark_apply/).

Como os clusters de Big Data usam conexões Livy, você deve definir `packages = FALSE` na chamada para **spark_apply**. Para obter mais informações, confira a seção [Livy](https://spark.rstudio.com/guides/distributed-r/#livy) da documentação do sparklyr sobre computações do R distribuídas. Com essa configuração, você só pode usar os pacotes do R que já estão instalados em seu cluster do Spark no código R passado para **spark_apply**. O seguinte exemplo demonstra esta funcionalidade:

```r
iris_tbl %>% spark_apply(function(e) nrow(e), names = "nrow", group_by = "Species", packages = FALSE)
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md).
