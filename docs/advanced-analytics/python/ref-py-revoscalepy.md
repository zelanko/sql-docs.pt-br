---
title: pacote revoscalepy Python
description: Introdução ao módulo revoscalepy no SQL Server Serviços de Machine Learning com Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 76c68d0753c4ba29387b3378c1086ce9bce4f53b
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715772"
---
# <a name="revoscalepy-python-module-in-sql-server"></a>revoscalepy (módulo python no SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**revoscalepy** é um módulo compatível com Python35 da Microsoft que dá suporte a computação distribuída, contextos de computação remota e algoritmos de ciência de dados de alto desempenho. Ele se baseia no pacote **RevoScaleR** para R (distribuído com Microsoft R Server e SQL Server R Services), oferecendo funcionalidade semelhante:

+ Contextos de computação local e remota em sistemas com a mesma versão do **revoscalepy**
+ Funções de visualização e transformação de dados
+ Funções de ciência de dados, escalonáveis por meio de processamento distribuído ou paralelo
+ Melhor desempenho, incluindo o uso das bibliotecas de matemática Intel

As fontes de dados e os contextos de computação que você cria no **revoscalepy** também podem ser usados em algoritmos de aprendizado de máquina. Para obter uma introdução a esses algoritmos, consulte [Microsoftml Python module in SQL Server](ref-py-microsoftml.md).

## <a name="full-reference-documentation"></a>Documentação de referência completa

A biblioteca **revoscalepy** é distribuída em vários produtos da Microsoft, mas o uso é o mesmo se você obter a biblioteca em SQL Server ou em outro produto. Como as funções são as mesmas, a [documentação para funções individuais revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) é publicada em apenas um local sob a [referência do Python](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para Microsoft Machine Learning Server. Se existirem comportamentos específicos do produto, as discrepâncias serão indicadas na página de ajuda da função.

## <a name="versions-and-platforms"></a>Versões e plataformas

O módulo **revoscalepy** se baseia no Python 3,5 e está disponível somente quando você instala um dos seguintes produtos ou downloads da Microsoft:

+ [Serviços de aprendizado de máquina do SQL Server](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 ou posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Bibliotecas de cliente Python para um cliente de ciência de dados](setup-python-client-tools-sql.md)

> [!NOTE]
> As versões completas de lançamento do produto são somente Windows, a partir do SQL Server 2017. O suporte do Linux para **revoscalepy** é novo na versão [prévia do SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="functions-by-category"></a>Funções por categoria

Esta seção lista as funções por categoria para dar uma ideia de como cada uma é usada. Você também pode [usar o Sumário](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para localizar funções em ordem alfabética.

## <a name="1-data-source-and-compute"></a>1-fonte de dados e computação

o **revoscalepy** inclui funções para criar fontes de dados e definir o local, ou o *contexto de computação*, de onde as computações são executadas. Funções relevantes para SQL Server cenários são listadas na tabela a seguir.

SQL Server e python usam tipos de dados diferentes em alguns casos. Para obter uma lista de mapeamentos entre tipos de dados SQL e Python, consulte [tipos de dados Python-to-SQL](python-libraries-and-data-types.md).

| Função| Descrição|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  Crie um objeto de contexto de computação SQL Server para enviar computações por push a uma instância remota. Várias funções **revoscalepy** usam o contexto de computação como um argumento. Para um exemplo de alternância de contexto, consulte [criar um modelo usando revoscalepy](../tutorials/use-python-revoscalepy-to-create-model.md).|
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | Crie um objeto de dados com base em uma SQL Server consulta ou tabela. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| Crie uma fonte de dados com base em uma conexão ODBC. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | Crie uma fonte de dados com base em um arquivo XDF local. Os arquivos XDF geralmente são usados para descarregar dados na memória para o disco. Um arquivo XDF pode ser útil ao trabalhar com mais dados do que pode ser transferido do banco de dado em um lote ou mais dados do que podem caber na memória. Por exemplo, se você mover regularmente grandes quantidades de dados de um banco de dados para uma estação de trabalho local, em vez de consultar o banco de dado repetidamente para cada operação de R, poderá usar o arquivo XDF como um tipo de cache para salvar os dados localmente e, em seguida, trabalhar com eles em seu espaço de trabalho do R. |

> [!TIP]
> Se você for novo na ideia de fontes de dados ou contextos de computação, recomendamos que comece com a [computação distribuída](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) na documentação do Microsoft Machine Learning Server.

## <a name="2-data-manipulation-etl"></a>2-manipulação de dados (ETL)

| Função | Descrição |
|----------|-------------|
|[rx_import](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-import) | Importe dados para um arquivo. Xdf ou quadro de dados.|
|[rx_data_step](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-data-step) | Transformar dados de um conjunto de dados de entrada em um conjunto de dados de saída.|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3-treinamento e Resumo

| Função| Descrição|
| ------- | ---------- |
|[rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) | Ajustar árvores de decisão aprimoradas do gradiente estocástico|
|[rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) | Ajustar as florestas de decisão de classificação e regressão|
|[rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) | Ajustar árvores de classificação e regressão |
|[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | Criar um modelo de regressão linear|
|[rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) | Criar um modelo de regressão logística|
|[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) | Produzir resumos de monovariável de objetos no revoscalepy.|

Você também deve examinar as funções no [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) para obter abordagens adicionais.

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>4-funções de Pontuação

| Função| Descrição|
| ------- | ---------- |
| [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | Gerar previsões de um modelo treinado|) | Gera previsões de um modelo treinado e pode ser usada para pontuação em tempo real. |
|[rx_predict_default](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | Computar valores previstos e resíduos usando objetos rx_lin_mod e rx_logit. |
|[rx_predict_rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | Calcule os valores previstos ou ajustados para um conjunto de dados de um objeto rx_dforest ou rx_btrees. |
|[rx_predict_rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | Calcule valores previstos ou ajustados para um conjunto de dados de um objeto rx_dtree. |

## <a name="how-to-work-with-revoscalepy"></a>Como trabalhar com o revoscalepy

As funções no **revoscalepy** são chamáveis no código Python encapsulado em procedimentos armazenados. A maioria dos desenvolvedores cria soluções **revoscalepy** localmente e, em seguida, migra o código Python concluído para procedimentos armazenados como um exercício de implantação.

Ao executar localmente, você normalmente executa um script Python na linha de comando ou em um ambiente de desenvolvimento do Python e especifica um SQL Server contexto de computação usando uma das funções **revoscalepy** . Você pode usar o contexto de computação remota para todo o código ou para funções individuais. Por exemplo, talvez você queira descarregar o treinamento do modelo para o servidor para usar os dados mais recentes e evitar a movimentação de dados.

Quando você estiver pronto para encapsular o script do Python dentro de um procedimento armazenado, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), é recomendável reescrever o código como uma única função que tenha entradas e saídas claramente definidas. 

As entradas e saídas devem ser quadros de dados pandas. Quando isso for feito, você poderá chamar o procedimento armazenado de qualquer cliente que ofereça suporte a T-SQL, passar consultas SQL facilmente como entradas e salvar os resultados em tabelas SQL. Para obter um exemplo, consulte [Learn in-Database Python Analytics for SQL Developers](../tutorials/sqldev-in-database-python-for-sql-developers.md).

### <a name="using-revoscalepy-with-microsoftml"></a>Usando revoscalepy com microsoftml

As funções do Python para [microsoftml](ref-py-microsoftml.md) são integradas aos contextos de computação e fontes de dados que são fornecidos no revoscalepy. Ao chamar funções de microsoftml, por exemplo, ao definir e treinar um modelo, use as funções revoscalepy para executar o código Python localmente ou em um contexto de computação remota do SQl Server.

O exemplo a seguir mostra a sintaxe para importar módulos em seu código Python. Em seguida, você pode fazer referência às funções individuais necessárias.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>Confira também

+ [Tutoriais do Python](../tutorials/sql-server-python-tutorials.md)
+ [Tutorial: Inserir código Python no T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Referência do Python (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)
