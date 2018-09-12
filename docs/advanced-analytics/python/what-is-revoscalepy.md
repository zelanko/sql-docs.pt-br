---
title: Introdução ao pacote do Python revoscalepy no aprendizado de máquina do SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f1d4d8bbb47c34fce61bdb95a3184a1d2b10f4d1
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889472"
---
# <a name="introducing-revoscalepy-in-sql-server-machine-learning"></a>Introdução ao revoscalepy no aprendizado de máquina do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**revoscalepy** é uma nova biblioteca do Python fornecidas pela Microsoft para dar suporte à computação distribuída, remoto contextos de computação e algoritmos de alto desempenho para desenvolvedores de Python.

Ele se baseia a **RevoScaleR** pacote para R, que foi fornecido no Microsoft R Server e SQL Server R Services e tem como objetivo fornecer a mesma funcionalidade:

+ Dá suporte a vários contextos de computação locais e remotos
+ Fornece funções equivalentes do RevoScaleR para visualização e transformação de dados
+ Fornece versões do Python de algoritmos de aprendizado de máquina do RevoScaleR para processamento distribuído ou paralelo
+ Desempenho aprimorado, incluindo o uso das bibliotecas de matemática da Intel

MicrosoftML pacotes também são fornecidos para R e Python. Para obter mais informações, consulte [usando MicrosoftML no SQL Server](../using-the-microsoftml-package.md)

## <a name="versions-and-supported-platforms"></a>As versões e plataformas com suporte

O **revoscalepy** módulo está disponível apenas quando você instala um dos seguintes produtos Microsoft:

+ Machine Learning Services no SQL Server 2017
+ Microsoft Machine Learning Server 9.2.0 ou posterior

Para obter a versão mais recente do revoscalepy, instale a atualização cumulativa 1 para SQL Server 2017. Ele inclui vários aprimoramentos no Python, incluindo:

+ Uma nova função de Python, `rx_create_col_info`, que obtém informações de esquema de uma fonte de dados do SQL Server, como [rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo) para 
+ Aprimoramentos [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) para dar suporte a cenários paralelos usando o `RxLocalParallel` contexto de computação. 

## <a name="supported-functions-and-data-types"></a>Tipos de dados e funções com suporte

Esta seção fornece uma visão geral dos tipos de dados do Python e novas funções de Python tem suportadas nas **revoscalepy** módulo, a partir da versão do SQL Server 2017 CTP 2.0. 

Para obter a lista mais recente de funções nas bibliotecas do Python liberadas até o momento, consulte estes links:

+ [revoscalepy para Python](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)

+ [microsoftml para Python](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)

### <a name="data-types-data-sources-and-compute-contexts"></a>Tipos de dados, fontes de dados e contextos de computação

SQL Server e o Python usa diferentes tipos de dados em alguns casos. Para obter uma lista de mapeamentos entre tipos de dados SQL e Python, consulte [extensão do Python](../concepts/extension-python.md).

Fontes de dados com suporte para o aprendizado de máquina com Python no SQL Server inclui os arquivos locais, incluindo arquivos XDF, banco de dados do SQL Server e fontes de dados ODBC.

Você pode criar o objeto de fonte de dados usando as funções listadas na tabela a seguir. Depois de definir a fonte de dados, você pode carregar ou transformar os dados usando um apropriado [função ETL](#bkmk_etl).

> [!IMPORTANT]
> Muitos nomes de função foram alterados desde a versão inicial do Python no CTP 2.0.

**Dados do SQL Server**

+ Use [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) para definir uma fonte de dados de uma consulta ou tabela
+ Use [RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserver) para criar um contexto de computação do SQL Server
+ Use [RxOdbcData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxodbcdata) para criar uma fonte de dados de uma conexão ODBC

**revoscalepy** também oferece suporte a [fonte de dados do XDF](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxxdfdata), usado para mover dados entre a memória e outras fontes de dados.

> [!TIP]
> Se você estiver familiarizado com a ideia de fontes de dados ou contextos de computação, é recomendável que você comece lendo sobre funciona de computação distribuída para o aprendizado de máquina no [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction).


### <a name="bkmk_algorithms"></a>Aprendizado de máquina e funções de resumo

Os seguintes algoritmos de aprendizado de máquina e o resumo de funções de RevoScaleR estão incluídas no SQL Server 2017, a partir do CTP 2.0.

| Função| Description|Observações|
| ------ | ------ |------ |
|`rx_btrees` | Ajustar as árvores de decisão aumentada de gradiente estocástico|`rx_btrees_ex` No CTP 2.0|
|`rx_dforest` | Ajustar as florestas de decisão de regressão e classificação|`rx_dforest_ex` No CTP 2.0|
|`rx_dtree` | Ajuste de árvores de regressão e classificação |`rx_dtree_ex` No CTP 2.0|
|`rx_lin_mod` | Criar um modelo linear|`rx_lin_mod_ex` No CTP 2.0|
|`rx_logit` | Criar um modelo de regressão logística|`rx_logit_ex` No CTP 2.0|
|`rx_predict` | Gerar previsões para um modelo treinado|`rx_predict_ex` No CTP 2.0|
|`rx_summary` | Gerar um resumo do modelo||

Novos algoritmos de aprendizado de máquina também são fornecidos pela versão do Python [MicrosoftML](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package):

| Função| Description|
| ------ | ------ |
|`rx_fast_forest` |Criar um modelo de floresta de decisão|
|`rx_fast_linear` | Regressão linear com coordenada dupla alheatória|
|`rx_fast_trees` | Criar um modelo de árvore aumentada |
|`rx_logistic_regression` | Criar um modelo de regressão logística|
|`rx_neural_network` | Criar um modelo de rede neural personalizável |
|`rx_oneclass_svm` | Cria um modelo SVM em um conjunto de dados em desequilíbrio, para uso na detecção de anomalias|

> [!TIP]
> Muitos desses algoritmos já são fornecidos como módulos no Azure Machine Learning.

MicrosoftML para Python também inclui uma variedade de transformações e funções auxiliares, como:

+ `rx_predict` gera previsões de um modelo treinado e pode ser usado para pontuação em tempo real
+ funções de personalização de imagem
+ funções para extração de processamento e o sentimento do texto

Para obter detalhes, consulte [Introdução ao MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)


> [!NOTE]
> A comunidade do Python usa as convenções de codificação que podem ser diferentes da que você está acostumado, incluindo todas as letras minúsculas e sublinhados em vez de concatenação com maiusculas e minúsculas para nomes de parâmetro. Além disso, talvez você tenha observado que o **revoscalepy** biblioteca é sempre minúscula. Está certo! Outra convenção de Python.
> 
> Confira as dicas sobre a documentação de referência de Python para o Microsoft R: [Ajuda da função Python][ajuda de função de Python](https://docs.microsoft.com/r-server/python-reference/introducing-python-package-reference)

## <a name="examples"></a>Exemplos

Você pode executar o código que inclui **revoscalepy** funções localmente ou em um contexto de computação remota. Você também pode executar o Python no SQL Server inserindo o código do Python em um procedimento armazenado.

Ao executar localmente, você normalmente executar um script Python de linha de comando ou de um ambiente de desenvolvimento do Python e especificar um contexto de computação do SQL Server usando um dos **revoscalepy** funções. Você pode usar o contexto de computação remota para todo o código, ou para funções individuais. Por exemplo, você talvez queira descarregamento de treinamento do modelo para o servidor para usar os dados mais recentes e evitar a movimentação de dados.

Se você deseja colocar um script Python completo dentro do procedimento armazenado, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), é recomendável que você reescreva o código como uma única função que claramente definida entradas e saídas. Entradas e saídas devem ser **pandas** quadros de dados. Quando isso for feito, você pode chamar o procedimento armazenado de qualquer cliente que dá suporte a T-SQL, facilmente passar consultas SQL como entradas e salvar os resultados em tabelas SQL. Por exemplo, consulte [análise do Python no banco de dados para desenvolvedores do SQL](../tutorials/sqldev-in-database-python-for-sql-developers.md).

### <a name="using-remote-compute-contexts"></a>Usando contextos de computação remota

+ [Criar um modelo usando revoscalepy](../tutorials/use-python-revoscalepy-to-create-model.md)

  Este exemplo demonstra como executar o Python usando uma instância do SQL Server como o contexto de computação.

### <a name="using-a-stored-procedure"></a>Usando um procedimento armazenado

+ [Executar Python usando T-SQL](../tutorials/run-python-using-t-sql.md)

  Este exemplo demonstra o mecanismo básico de chamada de script do Python que é inserido em um procedimento armazenado.

### <a name="using-revoscalepy-with-microsoftml"></a>Usando revoscalepy com MicrosoftML

As funções do Python para o MicrosoftML são integradas com as fontes de dados que são fornecidos no revoscalepy e contextos de computação. Portanto, você poderia usar um algoritmo MicrosoftML para definir e treinar um modelo em Python e usam as funções de revoscalepy para executar o código Python localmente ou em um contexto de computação do SQl Server.

Importar apenas os módulos em seu código Python e, em seguida, fazer referência a funções individuais que você precisa.

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

### <a name="requirements"></a>Requisitos

Para executar o código do Python no SQL Server, você deve ter instalado o SQL Server 2017 junto com o recurso **serviços de Machine Learning**e habilitado a linguagem Python. Versões anteriores do SQL Server não dão suporte a integração do Python.

> [!NOTE]
> Distribuições de software livre de Python não dão suporte a contextos de computação do SQL Server. No entanto, se você precisar publicar e consumir aplicativos de Python do Windows, você pode instalar o Microsoft Machine Learning Server sem instalar o SQL Server. Para obter mais informações, consulte [instalar o SQL Server 2017 Machine Learning Server (autônomo)](../install/sql-machine-learning-standalone-windows-install.md).

## <a name="get-more-help"></a>Obter mais ajuda

A documentação completa para essas APIs estarão disponível quando o produto é lançado. Enquanto isso, é recomendável que você referencie a função correspondente nas bibliotecas de RevoScaleR ou MicrosoftML.

+ [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler).
+ [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)

Você pode obter ajuda sobre qualquer função de Python, importando o módulo e, em seguida, chamar `help()`. Por exemplo, executando `help(revoscalepy)` em seu IDE do Python retorna uma lista de todas as funções no módulo revoscalepy, com suas assinaturas.

Se você usar as ferramentas Python para Visual Studio, você pode usar o IntelliSense para obter ajuda de sintaxe e o argumento. Para obter mais informações, consulte [suporte do Python no Visual Studio](http://docs.microsoft.com/visualstudio/python/installation)e baixar a extensão que corresponde à sua versão do Visual Studio. Você pode usar o Python com o Visual Studio 2015 e 2017 ou versões anteriores.

## <a name="see-also"></a>Consulte também

[Tutoriais do Python](../tutorials/sql-server-python-tutorials.md)
