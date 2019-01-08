---
title: revoscalepy pacote do Python - serviços do SQL Server Machine Learning
description: Introdução ao módulo revoscalepy em serviços do SQL Server 2017 Machine Learning com o Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b204ab644e4b454bc3671801f32b089a8210c521
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645166"
---
# <a name="revoscalepy-python-module-in-sql-server"></a>revoscalepy (módulo de Python no SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**revoscalepy** é um módulo Python35 compatível da Microsoft que oferece suporte à computação distribuída, contextos de computação remota e algoritmos de ciência de dados de alto desempenho. Ele se baseia a **RevoScaleR** pacote para o R (distribuída com Microsoft R Server e SQL Server R Services), oferecendo uma funcionalidade semelhante:

+ Contextos em sistemas com a mesma versão de computação local e remoto **revoscalepy**
+ Funções de transformação e visualização de dados
+ Funções de ciência de dados, escalonáveis por meio do processamento paralelo ou distribuído
+ Desempenho aprimorado, incluindo o uso das bibliotecas de matemática da Intel

Fontes de dados e contextos de computação que você cria no **revoscalepy** também pode ser usado em algoritmos de aprendizado de máquina. Para obter uma introdução a esses algoritmos, consulte [microsoftml módulo de Python no SQL Server](ref-py-microsoftml.md).

## <a name="full-reference-documentation"></a>Documentação de referência completo

O **revoscalepy** biblioteca é distribuída em vários produtos da Microsoft, mas o uso é o mesmo se você obter a biblioteca no SQL Server ou outro produto. Porque as funções são iguais, [documentação para funções individuais revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) é publicado para apenas um local sob a [referência de Python](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para Microsoft Machine Learning Server. Deve qualquer produto específico comportamentos existirem, serão observadas o discrepâncias na página de ajuda de função.

## <a name="versions-and-platforms"></a>As versões e plataformas

O **revoscalepy** módulo é com base em Python 3.5 e está disponível apenas quando você instala um dos seguintes produtos da Microsoft ou downloads:

+ [Serviços de aprendizado de máquina do SQL Server 2017](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 ou posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Bibliotecas de cliente do Python para um cliente de ciência de dados](setup-python-client-tools-sql.md)

> [!NOTE]
> São versões de lançamento de produto completo somente Windows, começando com o SQL Server 2017. Suporte do Linux para **revoscalepy** há de novo no [visualização do SQL Server de 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="functions-by-category"></a>Funções por categoria

Esta seção lista as funções por categoria para lhe dar uma ideia de como cada um deles é usado. Você também pode usar o [sumário](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para localizar funções em ordem alfabética.

## <a name="1-data-source-and-compute"></a>Computação e a fonte de dados 1

**revoscalepy** inclui funções para criar fontes de dados e definir o local, ou *contexto de computação*, de onde os cálculos são executados. Funções relevantes para cenários do SQL Server são listadas na tabela a seguir.

SQL Server e o Python usa diferentes tipos de dados em alguns casos. Para obter uma lista de mapeamentos entre tipos de dados SQL e Python, consulte [tipos de dados do Python-to-SQL](python-libraries-and-data-types.md).

| Função| Descrição|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  Crie um objeto de contexto de computação do SQL Server para enviar cálculos para uma instância remota. Vários **revoscalepy** funções usam um contexto de computação como um argumento. Para obter um exemplo de alternância de contexto, consulte [criar um modelo usando revoscalepy](../tutorials/use-python-revoscalepy-to-create-model.md).|
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | Crie um objeto de dados com base em uma consulta do SQL Server ou table. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| Crie uma fonte de dados com base em uma conexão ODBC. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | Crie uma fonte de dados com base em um arquivo XDF local. Arquivos XDF geralmente são usados para descarregar dados na memória em disco. Um arquivo XDF pode ser útil ao trabalhar com mais dados que podem ser transferidos do banco de dados em um lote ou mais dados do que pode caber na memória. Por exemplo, se você move regularmente grandes quantidades de dados de um banco de dados para uma estação de trabalho local, em vez de consultar o banco de dados repetidamente para cada operação de R, você pode usar o arquivo XDF como um tipo de cache para salvar os dados localmente e, em seguida, trabalhar com eles no seu espaço de trabalho do R. |

> [!TIP]
> Se você estiver familiarizado com a ideia de fontes de dados ou contextos de computação, é recomendável que você comece com [computação distribuída](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) na documentação do Microsoft Machine Learning Server.

## <a name="2-data-manipulation-etl"></a>Manipulação de dados 2 (ETL)

| Função | Descrição |
|----------|-------------|
|[rx_import](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-import) | Importar dados para um quadro de dados ou arquivo. xdf.|
|[rx_data_step](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-data-step) | Transforme dados de um conjunto de dados de entrada para um conjunto de dados de saída.|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3-treinamento e resumo

| Função| Descrição|
| ------- | ---------- |
|[rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) | Ajustar as árvores de decisão aumentada de gradiente estocástico|
|[rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) | Ajustar as florestas de decisão de regressão e classificação|
|[rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) | Ajuste de árvores de regressão e classificação |
|[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | Criar um modelo de regressão linear|
|[rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) | Criar um modelo de regressão logística|
|[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) | Produza resumos de monovariável de objetos em revoscalepy.|

Você também deve examinar as funções na [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) para outras abordagens.

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>Funções de pontuação de 4

| Função| Descrição|
| ------- | ---------- |
| [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | Gerar previsões para um modelo treinado|) | Gera previsões de um modelo treinado e pode ser usado para pontuação em tempo real. |
|[rx_predict_default](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | Os valores previstos e usando objetos rx_lin_mod e rx_logit de resíduos de computação. |
|[rx_predict_rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | Calcule valores previstos ou ajustados para um conjunto de dados de um objeto rx_dforest ou rx_btrees. |
|[rx_predict_rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | Calcule valores previstos ou ajustados para um conjunto de dados de um objeto rx_dtree. |

## <a name="how-to-work-with-revoscalepy"></a>Como trabalhar com revoscalepy

Funções em **revoscalepy** podem ser chamados no código do Python encapsulado em procedimentos armazenados. A maioria dos desenvolvedores construir **revoscalepy** localmente, soluções e, em seguida, migrar o código do Python concluído para procedimentos armazenados como um exercício de implantação.

Ao executar localmente, você normalmente executar um script Python de linha de comando ou de um ambiente de desenvolvimento do Python e especificar um contexto de computação do SQL Server usando um dos **revoscalepy** funções. Você pode usar o contexto de computação remota para todo o código, ou para funções individuais. Por exemplo, você talvez queira descarregamento de treinamento do modelo para o servidor para usar os dados mais recentes e evitar a movimentação de dados.

Quando você estiver pronto para encapsular o script de Python dentro de um procedimento armazenado, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), é recomendável reescrever o código como uma única função que claramente definida entradas e saídas. 

Entradas e saídas devem ser **pandas** quadros de dados. Quando isso for feito, você pode chamar o procedimento armazenado de qualquer cliente que dá suporte a T-SQL, facilmente passar consultas SQL como entradas e salvar os resultados em tabelas SQL. Por exemplo, consulte [Aprenda a análise de Python no banco de dados para desenvolvedores do SQL](../tutorials/sqldev-in-database-python-for-sql-developers.md).

### <a name="using-revoscalepy-with-microsoftml"></a>Usando revoscalepy com microsoftml

O Python funciona para o [microsoftml](ref-py-microsoftml.md) são integrados com as fontes de dados e contextos de computação que são fornecidas no revoscalepy. Ao chamar funções do microsoftml, por exemplo quando definindo e treinar um modelo, use as funções revoscalepy para executar o Python código localmente ou contexto de computação em um SQl Server remoto.

O exemplo a seguir mostra a sintaxe para importação de módulos em seu código Python. Você pode fazer referência as funções individuais, que você precisa.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>Confira também

+ [Tutoriais do Python](../tutorials/sql-server-python-tutorials.md)
+ [Tutorial: Incorporar código Python no T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Referência de Python (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)
