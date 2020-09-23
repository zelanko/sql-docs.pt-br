---
title: Implantar código R em procedimentos armazenados
description: Insira o código de linguagem R em um procedimento armazenado do SQL Server para disponibilizá-lo a qualquer aplicativo cliente que tenha acesso a um banco de dados SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/28/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 81cc8f392275093f370a0dda12d1aaf1fca542e5
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288258"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>Colocar o código R em operação usando procedimentos armazenados nos Serviços de Machine Learning do SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Ao usar os recursos do R e do Python nos Serviços de Machine Learning do SQL Server, a abordagem mais comum para mover soluções para um ambiente de produção é inserir o código em procedimentos armazenados. Este artigo resume os principais pontos para o desenvolvedor do SQL considerar ao colocar o código R em operação usando o SQL Server.

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>Implantar o script pronto para produção usando o T-SQL e procedimentos armazenados

Tradicionalmente, a integração de soluções de ciência de dados significava uma recodificação extensiva para dar suporte a desempenho e integração. Os Serviços de Machine Learning do SQL Server simplificam essa tarefa porque os códigos do R e do Python podem ser executados no SQL Server e chamados usando procedimentos armazenados. Para obter mais informações sobre a mecânica de inserção de código em procedimentos armazenados, confira:

+ [Criar e executar scripts do R simples no SQL Server](../tutorials/quickstart-r-create-script.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

Um exemplo mais abrangente de implantação do código R em produção usando procedimentos armazenados pode ser encontrado no [Tutorial: Análise de dados do R para desenvolvedores de SQL](../../machine-learning/tutorials/r-taxi-classification-introduction.md)

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>Diretrizes para otimizar o código R para SQL

A conversão do código R no SQL será mais fácil se algumas otimizações forem feitas com antecedência no código R ou Python. Isso inclui evitar tipos de dados que causam problemas, evitar conversões de dados desnecessárias e reescrever o código R como uma única chamada de função que pode ser facilmente parametrizada. Para obter mais informações, consulte:

+ [Tipos de dados e bibliotecas do R](r-libraries-and-data-types.md)
+ [Usar funções auxiliares sqlrutils](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>Integrar R e Python com aplicativos

Considerando que você pode executar R ou Python de um procedimento armazenado, pode executar scripts de qualquer aplicativo que possa enviar uma instrução T-SQL e processar os resultados. Por exemplo, você pode retreinar um modelo conforme um agendamento usando a [tarefa Executar T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) no Integration Services ou usando outro agendador de trabalhos que possa executar um procedimento armazenado.

A pontuação é uma tarefa importante que pode ser facilmente automatizada ou iniciada usando aplicativos externos. Você treina o modelo com antecedência, usando R ou Python ou um procedimento armazenado e [salva o modelo em formato binário](../tutorials/walkthrough-build-and-save-the-model.md) em uma tabela. Em seguida, o modelo pode ser carregado em uma variável como parte de uma chamada de procedimento armazenado usando uma destas opções de pontuação do T-SQL:

+ [Pontuação em tempo real, otimizada para lotes pequenos
+ Pontuação de linha única, para chamar de um aplicativo
+ [Pontuação nativa](../predictions/native-scoring-predict-transact-sql.md), para previsão de lote rápida do SQL Server sem chamar R

Este tutorial fornece um exemplo de pontuação usando um procedimento armazenado nos modos de lote e de linha única:

+ [Instruções passo a passo completas da ciência de dados para R no SQL Server](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)


## <a name="boost-performance-and-scale"></a>Impulsionar o desempenho e a escala

Embora a linguagem R de software livre tenha limitações conhecidas em relação a grandes conjuntos de dados, as [APIs de pacote RevoScaleR](ref-r-revoscaler.md) incluídas com o serviço do Machine Learning do SQL Server podem operar em grandes conjuntos de dados e se beneficiar de computação no banco de dados com vários thread, vários núcleos e vários processos.

Se a solução R usa agregações complexas ou envolve grandes conjuntos de dados, você pode aproveitar as agregações de memória e os índices columnstore altamente eficientes do SQL Server, deixando o código R tratar do processamento dos cálculos estatísticos e das pontuações.

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>Adaptar o código R para outras plataformas ou contextos de computação

O mesmo código R que você executa em dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser usado em relação a outras fontes de dados, como Spark sobre HDFS, quando você usa a [opção de servidor autônomo](../install/sql-machine-learning-standalone-windows-install.md) na instalação do SQL Server ou quando instala o produto que não tem a marca SQL, Microsoft Machine Learning Server (anteriormente conhecido como **Microsoft R Server**):

+ [Documentação do Machine Learning Server](https://docs.microsoft.com/r-server/)
