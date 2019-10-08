---
title: Gravar funções avançadas do Python
titleSuffix: SQL Server Machine Learning Services
description: Neste guia de início rápido, saiba como escrever uma função do Python para computação estatística avançada com SQL Server Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e369e83c99543cc31287932a25949c2ddec98e89
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007716"
---
# <a name="quickstart-write-advanced-python-functions-with-sql-server-machine-learning-services"></a>Início Rápido: Escrever funções avançadas do Python com o SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este guia de início rápido descreve como inserir funções matemáticas do Python e utilitário em um procedimento armazenado do SQL com SQL Server Serviços de Machine Learning. As funções estatísticas avançadas que são complicadas de implementar no T-SQL podem ser feitas no Python com apenas uma única linha de código.

## <a name="prerequisites"></a>Pré-requisitos

- Este início rápido requer acesso a uma instância do SQL Server com [SQL Server serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) com a linguagem Python instalada.

  Sua instância de SQL Server pode estar em uma máquina virtual do Azure ou no local. Apenas esteja ciente de que o recurso de script externo está desabilitado por padrão, portanto, talvez seja necessário [habilitar o script externo](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificar se **SQL Server Launchpad serviço** está em execução antes de iniciar.

- Você também precisa de uma ferramenta para executar consultas SQL que contêm scripts Python. Você pode executar esses scripts usando qualquer ferramenta de consulta ou gerenciamento de banco de dados, desde que ele possa se conectar a uma instância de SQL Server e executar uma consulta T-SQL ou um procedimento armazenado. Este início rápido usa o [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Criar um procedimento armazenado para gerar números aleatórios

Para simplificar, vamos usar o pacote Python `numpy`, que é instalado e carregado por padrão no SQL Server Serviços de Machine Learning com Python instalado. O pacote contém centenas de funções para tarefas estatísticas comuns, entre elas, a função `random.normal`, que gera um número específico de números aleatórios usando a distribuição normal, dado um desvio padrão e uma média.

Por exemplo, o código Python a seguir retorna 100 números em uma média de 50, dado um desvio padrão de 3.

```Python
numpy.random.normal(size=100, loc=50, scale=3)
```

Para chamar essa linha de Python do T-SQL, adicione a função Python no parâmetro de script Python de `sp_execute_external_script`. A saída espera um quadro de dados, portanto, use `pandas` para convertê-lo.

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

Isso é fácil quando combinado com SQL Server. Você define um procedimento armazenado que obtém os argumentos do usuário e, em seguida, passa esses argumentos para o script do Python como variáveis.

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

- As linhas que seguem imediatamente mapeiam os nomes de parâmetro do SQL para os nomes de variável Python correspondentes.

Agora que você encapsuleu a função Python em um procedimento armazenado, você pode chamar facilmente a função e passar valores diferentes, desta forma:

```sql
EXECUTE MyPyNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-python-utility-functions-for-troubleshooting"></a>Usar funções do utilitário Python para solução de problemas

Os pacotes do Python fornecem uma variedade de funções utilitárias para investigar o ambiente atual do Python. Essas funções podem ser úteis se você estiver encontrando discrepâncias na maneira como seu código Python é executado em SQL Server e em ambientes externos.

Por exemplo, você pode usar funções de tempo do sistema no pacote `time` para medir a quantidade de tempo usada pelos processos do Python e analisar problemas de desempenho.

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

Para criar um modelo de aprendizado de máquina usando Python no SQL Server, siga este guia de início rápido:

> [!div class="nextstepaction"]
> [Início Rápido: Criar e pontuar um modelo de previsão em Python com SQL Server Serviços de Machine Learning @ no__t-0

Para obter mais informações sobre SQL Server Serviços de Machine Learning, consulte:

- [O que é SQL Server Serviços de Machine Learning (Python e R)?](../what-is-sql-server-machine-learning.md)
