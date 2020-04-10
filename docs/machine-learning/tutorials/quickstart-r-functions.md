---
title: 'Início Rápido: Funções do R'
description: Neste guia de início rápido, você aprenderá a usar funções matemáticas e utilitárias do R com os Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/27/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e67dcbc35bf5af88d2a7fab37f795cd5cc1d55d9
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116169"
---
# <a name="quickstart-r-functions-with-sql-server-machine-learning-services"></a>Início Rápido: Funções do R com os Serviços de Machine Learning do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Neste guia de início rápido, você aprenderá a usar funções matemáticas e utilitárias do R com os Serviços de Machine Learning do SQL Server. As funções estatísticas muitas vezes são complicadas de implementar no T-SQL, mas isso pode ser feito no R com apenas algumas linhas de código.

## <a name="prerequisites"></a>Pré-requisitos

- Este início rápido requer acesso a uma instância do SQL Server que tenha os [Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md) com a linguagem R instalada.

  A instância do SQL Server pode ser local ou em uma máquina virtual do Azure. Esteja ciente de que o recurso de script externo está desabilitado por padrão, portanto, talvez seja necessário [habilitar o script externo](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificar se o **serviço SQL Server Launchpad** está em execução antes de você começar.

- Você também precisa de uma ferramenta para executar consultas SQL que contenham scripts R. Você pode executar esses scripts usando qualquer ferramenta de consulta ou de gerenciamento de banco de dados, desde que ele possa se conectar a uma instância do SQL Server e executar uma consulta T-SQL ou um procedimento armazenado. Esse início rápido usa o [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Criar um procedimento armazenado para gerar números aleatórios

Para simplificar, vamos usar o pacote de `stats` do R, que é instalado e carregado por padrão em Serviços de Machine Learning do SQL Server que têm o R instalado. O pacote contém centenas de funções para tarefas estatísticas comuns, entre elas, a função `rnorm`, que gera um número específico de números aleatórios usando a distribuição normal, dado um desvio padrão e uma média.

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

Isso é fácil quando se trabalha em combinação com o SQL Server. Você define um procedimento armazenado que obtém os argumentos do usuário e, em seguida, passa esses argumentos para o script R como variáveis.

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

Por exemplo, você pode usar a função R `memory.limit()` para obter memória para o ambiente atual de R. Uma vez que o pacote `utils` é instalado, mas não carregado por padrão, primeiro é necessário usar a função `library()` para carregá-lo.

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
        library(utils);
        mymemory <- memory.limit();
        OutputDataSet <- as.data.frame(mymemory);'
    , @input_data_1 = N' ;'
WITH RESULT SETS (([Col1] int not null));
```

> [!TIP]
> Muitos usuários gostam de usar as funções de tempo do sistema em R, tais como `system.time` e `proc.time`, para capturar o tempo usado por processos de R e analisar problemas de desempenho. Para obter um exemplo, confira o tutorial [Criar recursos de dados](../tutorials/walkthrough-create-data-features.md), em que as funções de tempo do R são inseridas na solução.

## <a name="next-steps"></a>Próximas etapas

Para criar um modelo de machine learning usando o R no SQL Server, siga este guia de início rápido:

> [!div class="nextstepaction"]
> [Criar e pontuar um modelo de previsão no R com os Serviços de Machine Learning do SQL Server](quickstart-r-train-score-model.md)

Para obter mais informações sobre os Serviços de Machine Learning do SQL Server, confira:

- [O que são os Serviços de Machine Learning do SQL Server (Python e R)?](../what-is-sql-server-machine-learning.md)
