---
title: "Introdução ao revoscalepy | Microsoft Docs"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 65a9924c70cdcdc86ce855b62caa23d19b72dc6d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="introducing-revoscalepy"></a>Introdução ao revoscalepy

**revoscalepy** é uma nova biblioteca fornecido pela Microsoft para dar suporte a computação distribuída, de computação remota contextos e algoritmos de alto desempenho para Python.

Ele se baseia o **RevoScaleR** pacote para R, que foi fornecido no Microsoft R Server e SQL Server R Services e tem como objetivo fornecer a mesma funcionalidade:

+ Oferece suporte a vários contextos de computação locais e remotos
+ Fornece funções equivalentes às RevoScaleR para visualização e transformação de dados
+ Fornece versões do Python de algoritmos de aprendizagem de máquina de RevoScaleR para processamento paralelo ou distribuído
+ Desempenho aprimorado, incluindo o uso das bibliotecas de matemática Intel

MicrosoftML pacotes também são fornecidos para R e Python. Para obter mais informações, consulte [MicrosoftML usando no SQL Server](../using-the-microsoftml-package.md)

## <a name="versions-and-supported-platforms"></a>Versões e plataformas com suporte

O **revoscalepy** módulo está disponível apenas quando você instala um dos seguintes produtos Microsoft:

+ Serviços no SQL Server de 2017 de aprendizado de máquina
+ Aprendizado de máquina do Microsoft Server 9.2.0 ou posterior

Para obter a versão mais recente do revoscalepy, instale a atualização cumulativa 1 para SQL Server 2017. Ele inclui vários aprimoramentos em Python, incluindo:

+ Uma nova função de Python, `rx_create_col_info`, que obtém informações de esquema de uma fonte de dados do SQL Server, como [rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo) para 
+ Aprimoramentos para [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) para dar suporte a cenários paralelos usando o `RxLocalParallel` contexto de computação. 

## <a name="supported-functions-and-data-types"></a>Tipos de dados e funções com suporte

Esta seção fornece uma visão geral dos tipos de dados de Python e novas funções de Python com suporte no **revoscalepy** módulo, começando com a versão do SQL Server de 2017 CTP 2.0. 

Para obter a lista mais recente de funções nas bibliotecas do Python lançadas, consulte estes links:

+ [revoscalepy para Python](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)

+ [microsoftml para Python](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)

### <a name="data-types-data-sources-and-compute-contexts"></a>Tipos de dados, fontes de dados e contextos de computação

SQL Server e Python usa diferentes tipos de dados em alguns casos. Para obter uma lista de mapeamentos entre tipos de dados SQL e Python, consulte [Python bibliotecas e tipos de dados](python-libraries-and-data-types.md).

Fontes de dados com suporte para o aprendizado de máquina com Python no SQL Server inclui fontes de dados ODBC, o banco de dados do SQL Server e arquivos locais, incluindo arquivos XDF.

Você pode criar o objeto de fonte de dados usando as funções listadas na tabela a seguir. Depois de definir a fonte de dados, você pode carregar ou transformar os dados usando um apropriado [função ETL](#bkmk_etl).

> [!IMPORTANT]
> Muitos nomes de função foram alterados desde a versão inicial do Python no CTP 2.0.

**Dados do SQL Server**

+ Use [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) para definir uma fonte de dados de uma consulta ou tabela
+ Use [RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserver) para criar um contexto de computação do SQL Server
+ Use [RxOdbcData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxodbcdata) para criar uma fonte de dados de uma conexão ODBC

**revoscalepy** também oferece suporte a [fonte de dados XDF](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxxdfdata), usado para mover dados entre a memória e outras fontes de dados.

> [!TIP]
> Se você estiver familiarizado com o conceito de fontes de dados ou contextos de computação, recomendamos que você comece lendo sobre funciona computação distribuída para o aprendizado de máquina em [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction).


### <a name="bkmk_algorithms"></a>Aprendizado de máquina e funções de resumo

Os seguintes algoritmos de aprendizado de máquina e o resumo de funções de RevoScaleR são incluídas no SQL Server de 2017, começando com o CTP 2.0.

| Função| Description|Observações|
| ------ | ------ |------ |
|`rx_btrees` | Ajustar as árvores de decisão ampliada de gradiente estocástico|`rx_btrees_ex`No CTP 2.0|
|`rx_dforest` | Ajustar a classificação e regressão florestas de decisão|`rx_dforest_ex`No CTP 2.0|
|`rx_dtree` | Árvores de classificação e regressão de ajuste |`rx_dtree_ex`No CTP 2.0|
|`rx_lin_mod` | Criar um modelo linear|`rx_lin_mod_ex`No CTP 2.0|
|`rx_logit` | Criar um modelo de regressão logística|`rx_logit_ex`No CTP 2.0|
|`rx_predict` | Gerar previsões de um modelo treinado|`rx_predict_ex`No CTP 2.0|
|`rx_summary` | Gerar um resumo do modelo||

Novos algoritmos de aprendizado de máquina também são fornecidos pela versão do Python [MicrosoftML](https://docs.microsoft.com/en-us/r-server/python-reference/microsoftml/microsoftml-package):

| Função| Description|
| ------ | ------ |
|`rx_fast_forest` |Criar um modelo de floresta de decisão|
|`rx_fast_linear` | Regressão linear com estocástico ascendente coordenada dupla|
|`rx_fast_trees` | Criar um modelo de árvore aprimorado |
|`rx_logistic_regression` | Criar um modelo de regressão logística|
|`rx_neural_network` | Criar um modelo de rede neural personalizável |
|`rx_oneclass_svm` | Cria um modelo SVM em um conjunto de dados desequilibrado, para uso na detecção de anomalias|

> [!TIP]
> Muitos desses algoritmos já são fornecidos como módulos no aprendizado de máquina do Azure.

MicrosoftML para Python também inclui uma variedade de transformações e funções auxiliares, como:

+ `rx_predict`gera previsões de um modelo treinado e pode ser usado para pontuação em tempo real
+ funções de personalização de imagem
+ funções para extração de sensibilidade e processamento de texto

Para obter detalhes, consulte [Introdução ao MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)


> [!NOTE]
> A comunidade de Python usa convenções de codificação que podem ser diferentes do que você está acostumado, incluindo todas as letras minúsculas e sublinhados em vez de concatenação com maiusculas e minúsculas para nomes de parâmetro. Além disso, talvez você tenha notado que o **revoscalepy** biblioteca está sempre em minúsculas. É isso! Outra convenção de Python.
> 
> Confira as dicas sobre a documentação de referência do Python para o Microsoft R: [Ajuda da função Python][função Python](https://docs.microsoft.com/r-server/python-reference/introducing-python-package-reference)

## <a name="examples"></a>Exemplos

Você pode executar o código que inclui **revoscalepy** funções localmente ou em um contexto de computação remota. Você também pode executar o Python dentro do SQL Server inserindo código Python em um procedimento armazenado.

Quando em execução localmente, você normalmente executar um script de Python de linha de comando ou de um ambiente de desenvolvimento do Python e especificar um contexto de computação do SQL Server usando uma da **revoscalepy** funções. Você pode usar o contexto de computação remota para todo o código ou funções individuais. Por exemplo, você talvez queira descarregamento de treinamento de modelo para o servidor para usar os dados mais recentes e evita a movimentação de dados.

Se você deseja colocar um script de Python concluído dentro do procedimento armazenado, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), recomendamos que você reescreva o código como uma única função que claramente definida entradas e saídas. Entradas e saídas devem ser **pandas** quadros de dados. Quando isso for feito, você pode chamar o procedimento armazenado de qualquer cliente que dá suporte a T-SQL, facilmente passar consultas SQL como entradas e salvar os resultados em tabelas do SQL. Para obter um exemplo, consulte [análise de Python no banco de dados para desenvolvedores em SQL](../tutorials/sqldev-in-database-python-for-sql-developers.md).

### <a name="using-remote-compute-contexts"></a>Usando contextos de computação remota

+ [Criar um modelo usando revoscalepy](../tutorials/use-python-revoscalepy-to-create-model.md)

  Este exemplo demonstra como executar Python usando uma instância do SQL Server como o contexto de computação.

### <a name="using-a-stored-procedure"></a>Usando um procedimento armazenado

+ [Executar Python usando o T-SQL](../tutorials/run-python-using-t-sql.md)

  Este exemplo demonstra o mecanismo básico de chamada de script de Python é inserido em um procedimento armazenado.

### <a name="using-revoscalepy-with-microsoftml"></a>Usando revoscalepy com MicrosoftML

As funções do Python para MicrosoftML são integradas com as fontes de dados que são fornecidas no revoscalepy e contextos de computação. Portanto, você pode usar um algoritmo de MicrosoftML para definir e treinar um modelo em Python e usar as funções de revoscalepy para executar o código Python localmente ou em um contexto de computação do SQl Server.

Importar apenas os módulos em seu código Python e, em seguida, fazer referência as funções individuais, que você precisa.

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

### <a name="requirements"></a>Requisitos

Para executar o código Python no SQL Server, você deve ter instalado o SQL Server 2017 junto com o recurso **serviços de aprendizado de máquina**e habilitado a linguagem Python. Versões anteriores do SQL Server não dão suporte a integração do Python.

> [!NOTE]
> Distribuições de código aberto do Python não dão suporte para contextos de computação do SQL Server. No entanto, se você precisar publicar e consumir aplicativos Python do Windows, você pode instalar o servidor de aprendizado de máquina do Microsoft sem instalar o SQL Server. Para obter mais informações, consulte [criar um Standalone R Server](../r/create-a-standalone-r-server.md)

## <a name="get-more-help"></a>Obter mais ajuda

A documentação completa para essas APIs estarão disponível quando o produto é liberado. Enquanto isso, é recomendável que você referencie a função correspondente nas bibliotecas do RevoScaleR ou MicrosoftML.

+ [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler).
+ [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)

Você pode obter ajuda sobre qualquer função Python importando o módulo e, em seguida, chamar `help()`. Por exemplo, executando `help(revoscalepy)` do seu IDE Python retorna uma lista de todas as funções no módulo revoscalepy com suas assinaturas.

Se você usar as ferramentas Python para Visual Studio, você pode usar o IntelliSense para obter ajuda de sintaxe e o argumento. Para obter mais informações, consulte [suporte a Python no Visual Studio](http://docs.microsoft.com/visualstudio/python/installation)e baixar a extensão que corresponda à versão do Visual Studio. Você pode usar o Python com Visual Studio 2015 e 2017 ou versões anteriores.

## <a name="see-also"></a>Consulte também

[Tutoriais do Python](../tutorials/sql-server-python-tutorials.md)
