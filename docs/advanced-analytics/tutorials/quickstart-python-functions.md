---
title: 'Início Rápido: Escrever funções do Python'
titleSuffix: SQL Server Machine Learning Services
description: Neste início rápido, saiba como escrever uma função do Python para computação estatística avançada com os Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 08f43c6406d0ca2c95cc21a207cae63af6e86902
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727004"
---
# <a name="quickstart-write-advanced-python-functions-with-sql-server-machine-learning-services"></a>Início Rápido: Escrever funções avançadas do Python com os Serviços de Machine Learning do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este guia de início rápido descreve como inserir funções matemáticas do Python e funções utilitárias em um procedimento armazenado do SQL com os Serviços de Machine Learning do SQL Server. As funções estatísticas avançadas que são complicadas de implementar no T-SQL podem ser feitas no Python com apenas uma única linha de código.

## <a name="prerequisites"></a>Prerequisites

- Este início rápido requer acesso a uma instância do SQL Server que tenha os [Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md) com a linguagem Python instalada.

  A instância do SQL Server pode ser local ou em uma máquina virtual do Azure. Esteja ciente de que o recurso de script externo está desabilitado por padrão, portanto, talvez seja necessário [habilitar o script externo](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificar se o **serviço SQL Server Launchpad** está em execução antes de você começar.

- Você também precisa de uma ferramenta para executar consultas SQL que contenham scripts Python. Você pode executar esses scripts usando qualquer ferramenta de consulta ou de gerenciamento de banco de dados, desde que ele possa se conectar a uma instância do SQL Server e executar uma consulta T-SQL ou um procedimento armazenado. Esse início rápido usa o [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

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

- [O que são os Serviços de Machine Learning do SQL Server (Python e R)?](../what-is-sql-server-machine-learning.md)
