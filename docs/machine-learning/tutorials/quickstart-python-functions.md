---
title: 'Início Rápido: Funções do Python'
titleSuffix: SQL machine learning
description: Neste início rápido, você aprenderá a usar funções matemáticas e utilitárias do Python com o machine learning do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/28/2020
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: edd4ec79799cbb62c32c70a9d40236ffd4a76b73
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869991"
---
# <a name="quickstart-python-functions-with-sql-machine-learning"></a>Início Rápido: Funções do Python com o machine learning do SQL
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

Neste guia de início rápido, você aprenderá a usar as funções matemáticas e utilitárias do Python com os [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md), os [Serviços de Machine Learning da Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview) ou os [Clusters de Big Data do SQL Server](../../big-data-cluster/machine-learning-services.md). As funções estatísticas muitas vezes são complicadas de implementar no T-SQL, mas isso pode ser feito no Python com apenas algumas linhas de código.

## <a name="prerequisites"></a>Pré-requisitos

Para executar este início rápido, você precisará dos pré-requisitos a seguir.

- Um banco de dados SQL em uma destas plataformas:
  - [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md). Para instalá-lo, confira o [Guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md) ou o [Guia de instalação do Linux](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json).
  - Clusters de Big Data do SQL Server. Veja como [habilitar os Serviços de Machine Learning em Clusters de Big Data do SQL Server](../../big-data-cluster/machine-learning-services.md).
  - Serviços de Machine Learning da Instância Gerenciada de SQL do Azure. Para obter informações, confira a [Visão geral dos Serviços de Machine Learning da Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview).

- Uma ferramenta para executar consultas SQL que contenham scripts Python. Este início rápido usa o [Azure Data Studio](../../azure-data-studio/what-is.md).

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Criar um procedimento armazenado para gerar números aleatórios

Para simplificar, vamos usar o pacote `numpy` do Python, que é instalado e carregado por padrão. O pacote contém centenas de funções para tarefas estatísticas comuns, entre elas, a função `random.normal`, que gera um número específico de números aleatórios usando a distribuição normal, dado um desvio padrão e uma média.

Por exemplo, o código Python a seguir retorna 100 números em uma média de 50, dado um desvio padrão de 3.

```Python
numpy.random.normal(size=100, loc=50, scale=3)
```

Para chamar essa linha de Python do T-SQL, adicione a função do Python no parâmetro de script Python de `sp_execute_external_script`. A saída espera uma estrutura de dados, portanto, use o `pandas` para convertê-la.

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=100, loc=50, scale=3));
'
    , @input_data_1 = N'   ;'
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

E se você quiser facilitar a geração de um conjunto de números aleatórios diferente? Você define um procedimento armazenado que obtém os argumentos do usuário e, em seguida, passa esses argumentos para o script Python como variáveis.

```sql
CREATE PROCEDURE MyPyNorm (
      @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=mynumbers, loc=mymean, scale=mysd));
'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- A primeira linha define cada um dos parâmetros de entrada SQL necessários quando o procedimento armazenado é executado.

- A linha que começa com `@params` define todas as variáveis usadas pelo código Python e os tipos de dados SQL correspondentes.

- As linhas imediatamente após mapeiam os nomes de parâmetro SQL para os nomes de variável do Python correspondentes.

Agora que você encapsulou a função do Python em um procedimento armazenado, pode facilmente chamar a função e passar valores diferentes, como este:

```sql
EXECUTE MyPyNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-python-utility-functions-for-troubleshooting"></a>Usar funções utilitárias do Python para solução de problemas

Os pacotes do Python fornecem uma variedade de funções utilitárias para investigar o ambiente atual do Python. Essas funções poderão ser úteis se você estiver encontrando discrepâncias na maneira como o código Python é executado no SQL Server e em ambientes externos.

Por exemplo, você pode usar funções de tempo do sistema no pacote de `time` para medir a quantidade de tempo usada pelos processos do Python e analisar problemas de desempenho.

```sql
EXECUTE sp_execute_external_script
      @language = N'Python'
    , @script = N'
import time
start_time = time.time()

# Run Python processes

elapsed_time = time.time() - start_time
'
    , @input_data_1 = N' ;';
```

## <a name="next-steps"></a>Próximas etapas

Para criar um modelo de machine learning usando o Python com o machine learning do SQL, siga este início rápido:

> [!div class="nextstepaction"]
> [Início Rápido: Criar e pontuar um modelo preditivo no Python](quickstart-python-train-score-model.md)
