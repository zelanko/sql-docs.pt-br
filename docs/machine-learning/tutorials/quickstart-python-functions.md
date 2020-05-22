---
title: 'Início Rápido: Funções do Python'
description: Neste guia de início rápido, você aprenderá a usar funções matemáticas e utilitárias do Python com os Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/28/2020
ms.topic: quickstart
author: cawrites
ms.author: chadam
ms.reviewer: garye
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6afe1685956c43e30ace59f3e5cc794a2abbd88f
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606694"
---
# <a name="quickstart-python-functions-with-sql-server-machine-learning-services"></a>Início Rápido: Funções do Python com os Serviços de Machine Learning do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Neste início rápido, você aprenderá a usar funções matemáticas e utilitárias do Python com os [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) ou nos [Clusters de Big Data](../../big-data-cluster/machine-learning-services.md). As funções estatísticas muitas vezes são complicadas de implementar no T-SQL, mas isso pode ser feito no Python com apenas algumas linhas de código.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Neste início rápido, você aprenderá a usar funções matemáticas e utilitárias do Python com os [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md). As funções estatísticas muitas vezes são complicadas de implementar no T-SQL, mas isso pode ser feito no Python com apenas algumas linhas de código.
::: moniker-end

## <a name="prerequisites"></a>Pré-requisitos

- Este início rápido requer acesso a uma instância do SQL Server que tenha os [Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md) com a linguagem Python instalada.

  A instância do SQL Server pode ser local ou em uma máquina virtual do Azure. Esteja ciente de que o recurso de script externo está desabilitado por padrão, portanto, talvez seja necessário [habilitar o script externo](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificar se o **serviço SQL Server Launchpad** está em execução antes de você começar.

- Você também precisa de uma ferramenta para executar consultas SQL que contenham scripts Python. Você pode executar esses scripts usando qualquer ferramenta de consulta ou de gerenciamento de banco de dados, desde que ele possa se conectar a uma instância do SQL Server e executar uma consulta T-SQL ou um procedimento armazenado. Este início rápido usa o [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio).

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Criar um procedimento armazenado para gerar números aleatórios

Para simplificar, vamos usar o pacote de `numpy` do Python, que é instalado e carregado por padrão em Serviços de Machine Learning do SQL Server que têm o Python instalado. O pacote contém centenas de funções para tarefas estatísticas comuns, entre elas, a função `random.normal`, que gera um número específico de números aleatórios usando a distribuição normal, dado um desvio padrão e uma média.

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

E se você quiser facilitar a geração de um conjunto de números aleatórios diferente?

Isso é fácil quando se trabalha em combinação com o SQL Server. Você define um procedimento armazenado que obtém os argumentos do usuário e, em seguida, passa esses argumentos para o script Python como variáveis.

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

Para criar um modelo de machine learning usando o Python no SQL Server, siga este guia de início rápido:

> [!div class="nextstepaction"]
> [Início Rápido: Criar e pontuar um modelo de previsão no Python com os Serviços de Machine Learning do SQL Server](quickstart-python-train-score-model.md)

Para obter mais informações sobre os Serviços de Machine Learning do SQL Server, confira:

- [O que são os Serviços de Machine Learning do SQL Server (Python e R)?](../sql-server-machine-learning-services.md)
