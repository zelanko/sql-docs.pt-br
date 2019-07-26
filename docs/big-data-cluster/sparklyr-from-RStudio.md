---
title: Usar sparklyr de RStudio
titleSuffix: SQL Server big data clusters
description: Conecte-se ao cluster Big Data usando o sparklyr do RStudio.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 04/08/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f346fed17e4c79214a7eba43f70767fc80b98a07
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67728380"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>Usar sparklyr no cluster SQL Server Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O Sparklyr fornece uma interface R para Apache Spark. O Sparklyr é uma maneira popular para os desenvolvedores de R usarem o Spark. Este artigo descreve como usar o sparklyr em um cluster SQL Server 2019 Big Data (versão prévia) usando o RStudio.

## <a name="prerequisites"></a>Pré-requisitos

- [Implante um cluster SQL Server 2019 Big data](quickstart-big-data-cluster-deploy.md).

### <a name="install-rstudio-desktop"></a>Instalar o RStudio desktop

Instale e configure o **RStudio desktop** com as seguintes etapas:

1. Se você estiver executando o em um cliente do Windows, [Baixe e instale o R 3.4.4](https://cran.rstudio.com/bin/windows/base/old/3.4.4).

1. [Baixe e instale o RStudio desktop](https://www.rstudio.com/products/rstudio/download/).

1. Após a conclusão da instalação, execute os seguintes comandos dentro da área de trabalho do RStudio para instalar os pacotes necessários:

   ```RStudioDesktop
   install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## <a name="connect-to-spark-in-a-big-data-cluster"></a>Conectar-se ao Spark em um cluster Big Data

Você pode usar o sparklyr para se conectar de um cliente ao cluster Big Data usando o Livy e o gateway HDFS/Spark. 

No RStudio, crie um script R e conecte-se ao Spark como no exemplo a seguir:

> [!TIP]
> Para os `<USERNAME>` valores `<PASSWORD>` e, use o nome de usuário (como raiz) e a senha que você definiu durante a implantação de cluster Big Data. Para os `<IP>` valores `<PORT>` e, consulte a documentação sobre como [se conectar a um cluster Big data](connect-to-big-data-cluster.md).

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

## <a name="run-sparklyr-queries"></a>Executar consultas do sparklyr

Depois de se conectar ao Spark, você pode executar o sparklyr. O exemplo a seguir executa uma consulta no conjunto de uma íris usando sparklyr:

```r
iris_tbl <- copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="distributed-r-computations"></a>Cálculos de R distribuídos

Um recurso do sparklyr é a capacidade de [distribuir cálculos de R](https://spark.rstudio.com/guides/distributed-r/) com o [spark_apply](https://spark.rstudio.com/reference/spark_apply/).

Como os clusters Big data usam conexões Livy, você deve `packages = FALSE` definir na chamada para **spark_apply**. Para obter mais informações, consulte a [seção Livy](https://spark.rstudio.com/guides/distributed-r/#livy) da documentação do sparklyr sobre cálculos de R distribuídos. Com essa configuração, você só pode usar os pacotes do R que já estão instalados em seu cluster Spark no código R passado para **spark_apply**. O exemplo a seguir demonstra essa funcionalidade:

```r
iris_tbl %>% spark_apply(function(e) nrow(e), names = "nrow", group_by = "Species", packages = FALSE)
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters Big Data, consulte [o que são SQL Server 2019 Big data clusters](big-data-cluster-overview.md).
