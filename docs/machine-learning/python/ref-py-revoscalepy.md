---
title: Pacote revoscalepy do Python
description: Introdução ao módulo do revoscalepy nos Serviços de Machine Learning do SQL Server com o Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 145c1f571cc76bd8c26fc781ee7f4edcbfd3cb3a
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81117919"
---
# <a name="revoscalepy-python-module-in-sql-server"></a>revoscalepy (módulo do Python no SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O **revoscalepy** é um módulo compatível com o Python35 da Microsoft que dá suporte à computação distribuída, a contextos de computação remota e a algoritmos de ciência de dados de alto desempenho. Ele se baseia no pacote **RevoScaleR** para R (distribuído com o Microsoft R Server e o SQL Server R Services), oferecendo funcionalidade semelhante:

+ Contextos de computação local e remota em sistemas com a mesma versão do **revoscalepy**
+ Funções de visualização e transformação de dados
+ Funções de ciência de dados, escalonáveis por meio de processamento distribuído ou paralelo
+ Melhor desempenho, incluindo o uso das bibliotecas de matemática Intel

As fontes de dados e os contextos de computação criados no **revoscalepy** também podem ser usados em algoritmos de aprendizado de máquina. Para obter uma introdução a esses algoritmos, confira [Módulo microsoftml do Python no SQL Server](ref-py-microsoftml.md).

## <a name="full-reference-documentation"></a>Documentação de referência completa

A biblioteca do **revoscalepy** é distribuída em vários produtos da Microsoft, mas o uso é o mesmo com a biblioteca no SQL Server ou em outro produto. Como as funções são as mesmas, a [documentação para funções individuais do revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) é publicada em apenas uma localização na [referência do R](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para o Microsoft Machine Learning Server. Se existirem comportamentos específicos do produto, as discrepâncias serão indicadas na página de ajuda da função.

## <a name="versions-and-platforms"></a>Versões e plataformas

O módulo **revoscalepy** se baseia no Python 3.5 e está disponível somente quando você instala um dos seguintes produtos ou downloads da Microsoft:

+ [Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 ou posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Bibliotecas de clientes do Python para um cliente de ciência de dados](setup-python-client-tools-sql.md)

> [!NOTE]
> As versões completas do produto são somente Windows no SQL Server 2017. Há suporte no Windows e no Linux para o **revoscalepy** no [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="functions-by-category"></a>Funções por categoria

Esta seção lista as funções por categoria para dar uma ideia de como cada uma é usada. Use também o [sumário](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para localizar as funções em ordem alfabética.

## <a name="1-data-source-and-compute"></a>1 – Fonte de dados e computação

O **revoscalepy** inclui funções para criar fontes de dados e definir a localização ou o *contexto de computação*, de execução dos cálculos. Funções relevantes para cenários do SQL Server são listadas na tabela abaixo.

O SQL Server e o Python usam diferentes tipos de dados em alguns casos. Para obter uma lista de mapeamentos entre os tipos de dados SQL e Python, confira [Tipos de dados do Python para SQL](python-libraries-and-data-types.md).

| Função| Descrição|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  Crie um objeto de contexto de computação do SQL Server para efetuar push de cálculos para uma instância remota. Várias funções do **revoscalepy** usam o contexto de computação como argumento. Para obter um exemplo de alternância de contexto, confira [Criar um modelo usando revoscalepy](../tutorials/use-python-revoscalepy-to-create-model.md).|
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | Crie um objeto de dados com base em uma consulta ou uma tabela do SQL Server. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| Crie uma fonte de dados com base em uma conexão ODBC. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | Crie uma fonte de dados com base em um arquivo XDF local. Os arquivos XDF geralmente são usados para descarregar dados na memória no disco. Um arquivo XDF pode ser útil ao trabalhar com mais dados do que é possível transferir do banco de dados em um lote ou mais dados do que cabem na memória. Por exemplo, se você mover regularmente grandes quantidades de dados de um banco de dados para uma estação de trabalho local, em vez de consultar o banco de dados repetidamente para cada operação do R, use o arquivo XDF como um tipo de cache para salvar os dados localmente e, em seguida, trabalhar com eles no workspace do R. |

> [!TIP]
> Se a ideia de fontes de dados ou contextos de computação for uma novidade para você, recomendamos que comece com a [computação distribuída](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) na documentação do Microsoft Machine Learning Server.

## <a name="2-data-manipulation-etl"></a>2 – Manipulação de dados (ETL)

| Função | Descrição |
|----------|-------------|
|[rx_import](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-import) | Importe dados para um arquivo .xdf ou um quadro de dados.|
|[rx_data_step](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-data-step) | Transforme dados de um conjunto de dados de entrada em um conjunto de dados de saída.|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3 – Treinamento e resumo

| Função| Descrição|
| ------- | ---------- |
|[rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) | Ajuste árvores de decisão aumentadas de gradiente alheatórias|
|[rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) | Ajuste florestas de decisão de classificação e regressão|
|[rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) | Ajuste árvores de classificação e regressão |
|[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | Criar um modelo de regressão linear|
|[rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) | Criar um modelo de regressão logística|
|[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) | Produza resumos monovariáveis de objetos no revoscalepy.|

Examine também as funções no [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) para ver outras abordagens.

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>4 – Funções de pontuação

| Função| Descrição|
| ------- | ---------- |
| [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | Gere previsões com base em um modelo treinado|) | Gera previsões com base em um modelo treinado e pode ser usado para pontuação em tempo real. |
|[rx_predict_default](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | Calcule os valores previstos e os resíduos usando objetos rx_lin_mod e rx_logit. |
|[rx_predict_rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | Calcule os valores previstos ou ajustados para um conjunto de dados de um objeto rx_dforest ou rx_btrees. |
|[rx_predict_rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | Calcule os valores previstos ou ajustados para um conjunto de dados de um objeto rx_dtree. |

## <a name="how-to-work-with-revoscalepy"></a>Como trabalhar com o revoscalepy

As funções do **revoscalepy** podem ser chamadas no código Python encapsulado em procedimentos armazenados. A maioria dos desenvolvedores cria soluções do **revoscalepy** localmente e, em seguida, migra o código do Python concluído para procedimentos armazenados como um exercício de implantação.

Na execução local, normalmente, você executa um script Python na linha de comando ou em um ambiente de desenvolvimento do Python e especifica um contexto de computação do SQL Server usando uma das funções do **revoscalepy**. Use o contexto de computação remota para todo o código ou para funções individuais. Por exemplo, talvez você queira descarregar o treinamento do modelo no servidor para usar os dados mais recentes e evitar a movimentação de dados.

Quando você estiver pronto para encapsular o script Python dentro de um procedimento armazenado, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), recomendamos reescrever o código como uma única função que tenha entradas e saídas claramente definidas. 

As entradas e as saídas precisam ser quadros de dados **Pandas**. Quando isso for feito, você poderá chamar o procedimento armazenado em qualquer cliente que dê suporte a T-SQL, passar com facilidade consultas SQL como entradas e salvar os resultados em tabelas SQL. Para obter um exemplo, confira [Saiba mais sobre a análise do Python no banco de dados para desenvolvedores do SQL](../tutorials/sqldev-in-database-python-for-sql-developers.md).

### <a name="using-revoscalepy-with-microsoftml"></a>Como usar o revoscalepy com o microsoftml

As funções do Python para o [microsoftml](ref-py-microsoftml.md) são integradas às fontes de dados e aos contextos de computação fornecidos no revoscalepy. Ao chamar funções no microsoftml, por exemplo, ao definir e treinar um modelo, use as funções do revoscalepy para executar o código Python localmente ou em um contexto de computação remota do SQL Server.

O exemplo a seguir mostra a sintaxe para importar módulos no código Python. Em seguida, referencie as funções individuais necessárias.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>Confira também

+ [Tutoriais do Python](../tutorials/sql-server-python-tutorials.md)
+ [Referência do Python (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)
