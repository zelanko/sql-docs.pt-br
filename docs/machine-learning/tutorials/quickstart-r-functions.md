---
title: 'Início Rápido: Funções do R'
titleSuffix: SQL machine learning
description: Neste início rápido, você aprenderá a usar funções matemáticas e utilitárias do R com o aprendizado de máquina do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/21/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: d0c494602aca3cdcd40e27116f2a2b65e3ce5971
ms.sourcegitcommit: 49ee3d388ddb52ed9cf78d42cff7797ad6d668f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2020
ms.locfileid: "94384851"
---
# <a name="quickstart-r-functions-with-sql-machine-learning"></a>Início Rápido: Funções do R com o aprendizado de máquina do SQL
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Neste início rápido, você aprenderá a usar funções matemáticas e utilitárias do R com os [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) ou nos [Clusters de Big Data](../../big-data-cluster/machine-learning-services.md). As funções estatísticas muitas vezes são complicadas de implementar no T-SQL, mas isso pode ser feito no R com apenas algumas linhas de código.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Neste início rápido, você aprenderá a usar funções matemáticas e utilitárias do R com os [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md). As funções estatísticas muitas vezes são complicadas de implementar no T-SQL, mas isso pode ser feito no R com apenas algumas linhas de código.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Neste início rápido, você aprenderá a usar funções matemáticas e utilitárias do R com o [SQL Server R Services](../r/sql-server-r-services.md). As funções estatísticas muitas vezes são complicadas de implementar no T-SQL, mas isso pode ser feito no R com apenas algumas linhas de código.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
Neste início rápido, você aprenderá a usar estruturas de dados e tipos de dados ao usar R nos [Serviços de Machine Learning da Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview). Você aprenderá como mover dados entre o R e a Instância Gerenciada de SQL, bem como os problemas comuns que podem ocorrer.
::: moniker-end

## <a name="prerequisites"></a>Pré-requisitos

Para executar este início rápido, você precisará dos pré-requisitos a seguir.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
- Serviços de Machine Learning do SQL Server. Para saber como instalar os Serviços de Machine Learning, confira o [Guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md) ou o [Guia de instalação do Linux](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json). Você também pode [habilitar Serviços de Machine Learning em Clusters de Big Data do SQL Server](../../big-data-cluster/machine-learning-services.md).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
- Serviços de Machine Learning do SQL Server. Para saber como instalar os Serviços de Machine Learning, confira o [Guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md). 
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
- SQL Server 2016 R Services. Para saber como instalar o R Services, confira o [Guia de instalação do Windows](../install/sql-r-services-windows-install.md).
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
- Serviços de Machine Learning da Instância Gerenciada de SQL do Azure. Para saber como se inscrever, confira a [Visão geral dos Serviços de Machine Learning da Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview).
::: moniker-end

- Uma ferramenta para executar consultas SQL que contenham scripts do R. Este início rápido usa o [Azure Data Studio](../../azure-data-studio/what-is.md).

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Criar um procedimento armazenado para gerar números aleatórios

Para simplificar, vamos usar o pacote `stats` do R, que é instalado e carregado por padrão. O pacote contém centenas de funções para tarefas estatísticas comuns, entre elas, a função `rnorm`, que gera um número específico de números aleatórios usando a distribuição normal, dado um desvio padrão e uma média.

Por exemplo, o código R a seguir retorna 100 números em uma média de 50, dado um desvio padrão de 3.

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

Para chamar esta linha de R por meio do T-SQL, adicione a função do R no parâmetro de script R de `sp_execute_external_script`, deste modo:

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

E se você quiser facilitar a geração de um conjunto de números aleatórios diferente?

Isso é fácil quando se trabalha em combinação com o T-SQL. Você define um procedimento armazenado que obtém os argumentos do usuário e, em seguida, passa esses argumentos para o script R como variáveis.

```sql
CREATE PROCEDURE MyRNorm (
    @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynumbers, mymean, mysd));'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- A primeira linha define cada um dos parâmetros de entrada SQL necessários quando o procedimento armazenado é executado.

- A linha que começa com `@params` define todas as variáveis usadas pelo código R e os tipos de dados SQL correspondentes.

- As linhas imediatamente após mapeiam os nomes de parâmetro SQL para os nomes de variável R correspondentes.

Agora que você encapsulou a função R em um procedimento armazenado, pode facilmente chamar a função e passar valores diferentes, como este:

```sql
EXECUTE MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-r-utility-functions-for-troubleshooting"></a>Usar funções de utilitário de R para solução de problemas

O pacote **utilitários**, instalado por padrão, fornece uma variedade de funções utilitárias para investigar o ambiente de R atual. Essas funções poderão ser úteis se você estiver encontrando discrepâncias na maneira como o código R é executado no SQL Server e em ambientes externos.

Por exemplo, você pode usar as funções de tempo do sistema em R, como `system.time` e `proc.time`, para capturar o tempo usado por processos de R e analisar problemas de desempenho. Para obter um exemplo, confira o tutorial [Criar recursos de dados](../tutorials/walkthrough-create-data-features.md), em que as funções de tempo do R são inseridas na solução.

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
        library(utils);
        start.time <- proc.time();
        
        # Run R processes
        
        elapsed_time <- proc.time() - start.time;'
```

Para ver outras funções úteis, confira [Usar funções de criação de perfil de código R para aprimorar o desempenho](../r/using-r-code-profiling-functions.md).

## <a name="next-steps"></a>Próximas etapas

Para criar um modelo de machine learning usando o R com o aprendizado de máquina do SQL, siga este início rápido:

> [!div class="nextstepaction"]
> [Criar e pontuar um modelo de previsão no R com o aprendizado de máquina do SQL](quickstart-r-train-score-model.md)
