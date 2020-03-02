---
title: Modelagem preditiva com R
description: Este artigo descreve as melhorias no processo de ciência de dados possíveis por meio da integração com o SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6b336404d3b69e31ffb6f1a2aa82ade04804eb9e
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78172126"
---
# <a name="data-exploration-and-predictive-modeling-with-r-in-sql-server"></a>Exploração e Dados e Modelagem Preditiva com R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve as melhorias no processo de ciência de dados possíveis por meio da integração com o SQL Server.

## <a name="the-data-science-process"></a>O processo de ciência de dados

Cientistas de dados geralmente usam R para explorar dados e criar modelos preditivos. Esse geralmente é um processo iterativo de tentativa e erro até chegar a um bom modelo preditivo. Com um cientista de dados experiente, você pode se conectar ao banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e buscar os dados para sua estação de trabalho local usando o pacote RODBC, explorar seus dados e criar um modelo preditivo usando pacotes R padrão.

No entanto, essa abordagem tem muitas desvantagens, que prejudicaram a adoção mais ampla do R na empresa. 

+ A movimentação de dados pode ser lenta, ineficiente ou insegura
+ O R em si tem limitações de desempenho e escala

Essas desvantagens ficam mais aparentes quando você precisa mover e analisar grandes quantidades de dados ou usar conjuntos de dados que não cabem na memória disponível em seu computador.

Os pacotes e funções novos e escalonáveis do R inclusos com o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ajudam você a superar muitos desses desafios. 

## <a name="whats-different-about-revoscaler"></a>O que é diferente no RevoScaleR?

O pacote **RevoScaleR** contém implementações de algumas das funções R mais populares, que foram remodeladas para oferecer paralelismo e escalabilidade. Para obter mais informações, confira [Computação distribuída usando o RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing).

O pacote RevoScaleR também oferece suporte para alteração do *contexto de execução*. Isso significa que, para uma solução inteira ou apenas uma função, você pode indicar que computações devem ser realizadas usando os recursos do computador que hospeda a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em vez de sua estação de trabalho local. Essa abordagem tem diversas vantagens: você evita a movimentação desnecessária de dados e pode aproveitar mais recursos de computação no computador do servidor.

## <a name="r-environment-and-packages"></a>Pacotes e Ambiente R

O ambiente de R com suporte no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] consiste em um runtime, a linguagem de código aberto e um mecanismo gráfico com suporte e estendido por vários pacotes. A linguagem permite uma variedade de extensões que são implementadas usando pacotes.  

### <a name="using-other-r-packages"></a>Como usar outros pacotes do R

Além das bibliotecas do R proprietárias incluídas no Microsoft Machine Learning, você pode usar quase todos os pacotes do R em sua solução, incluindo:

+ Pacotes de R de finalidade geral de repositórios públicos. Você pode obter os pacotes R de código aberto de repositórios públicos populares, como o CRAN, que hospeda mais 6000 pacotes que podem ser usados por cientistas de dados.
  
  Para a plataforma Windows, os pacotes de R são fornecidos como arquivos zip e podem ser baixados e instalados sob a licença GPL.  
  
  Para saber mais sobre como instalar pacotes de terceiros para usar com o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], veja [Install Additional R Packages on SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
  
+ Pacotes e bibliotecas adicionais fornecidos pelo [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].   
  
     O pacote **RevoScaleR** inclui análise de alto desempenho de Big Data, versões aprimoradas de funções que dão suporte a tarefas comuns de ciência de dados, aprendizes otimizados para Naive Bayes, regressão linear, modelos de série temporal e redes neurais e bibliotecas matemáticas avançadas.  
  
     O pacote **RevoPemaR** permite que você desenvolva seus próprios algoritmos de memória externa paralela em R.  
  
     Para obter mais informações sobre esses pacotes e como usá-los, confira [O que é o RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-revoscaler) e [Introdução ao RevoPemaR](https://docs.microsoft.com/machine-learning-server/r/how-to-developer-pemar). 

+ O **MicrosoftML** contém uma coleção de algoritmos de aprendizado de máquina altamente otimizados e transformações de dados da equipe de Ciência de Dados da Microsoft. Muitos dos algoritmos também são usados no Azure Machine Learning. Para obter mais informações, confira [MicrosoftML no SQL Server](ref-r-microsoftml.md).

### <a name="r-development-tools"></a>Ferramentas de Desenvolvimento R

Ao desenvolver sua solução do R, baixe o Microsoft R Client. Este download gratuito inclui as bibliotecas necessárias para dar suporte a contextos de computação remota e algoritmos escalonáveis:

+ **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]:** Uma distribuição do runtime R e um conjunto de pacotes, como a biblioteca de kernel de matemática da Intel, que melhora o desempenho de operações R padrão.  
  
+ **RevoScaleR:** um pacote de R que lhe permite enviar computações por push a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]. Ele também inclui um conjunto de funções R comuns que foram reprojetadas para fornecer melhor desempenho e escalabilidade. Você pode identificar essas funções aprimoradas pelo prefixo **rx** . Ele também inclui provedores de dados aprimorados para uma variedade de fontes; essas funções são prefixadas com **Rx**.

Você pode usar qualquer editor de código baseado no Windows que dê suporte a R, como [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] ou RStudio. O download do [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] também inclui ferramentas de linha de comando comuns para R, como RGui.exe.

## <a name="use-new-data-sources-and-compute-contexts"></a>Usar novas fontes de dados e contextos de computação

Ao usar o pacote RevoScaleR para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], procure estas funções a serem usadas em seu código R:

+ **RxSqlServerData** é uma função fornecida no pacote RevoScaleR para oferecer suporte à conectividade de dados aprimorada com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
     Use essa função em seu código R para definir a *fonte de dados*. O objeto da fonte de dados especifica o servidor e as tabelas onde os dados residem e gerencia a tarefa de ler e gravar dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
-   O pacote **RxInSqlServer** pode ser usada para especificar o *contexto de computação*.  Em outras palavras, você pode indicar onde o código R deve ser executado: na sua estação de trabalho local ou no computador que hospeda a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  Para obter mais informações, confira [Funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler).
  
     Quando você define o contexto de computação, ele afeta somente os cálculos que dão suporte ao contexto de execução remota, o que significa as operações R fornecidas pelo pacote RevoScaleR e funções relacionadas. Normalmente, as soluções de R com base em pacotes CRAN padrão não podem ser executadas em um contexto de computação remota, embora possam ser executadas no computador [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] se iniciadas pelo T-SQL. No entanto, é possível usar a função `rxExec` para chamar funções de R individuais e executá-las remotamente em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

Para obter exemplos de como criar e trabalhar com fontes de dados e contextos de execução, confira estes tutoriais:

+ [Aprofundamento da ciência de dados](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)  
+  [Análise de dados usando o Microsoft R](https://docs.microsoft.com/machine-learning-server/r/how-to-introduction)

## <a name="deploy-r-code-to-production"></a>Implantar o código R em produção

Uma parte importante da ciência de dados é fornecer suas análises para outras pessoas ou usar modelos preditivos para melhorar os resultados ou processos de negócios. No [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], é fácil passar para a produção quando seu script ou modelo R estiver pronto.

Para saber mais sobre como mover seu código para executá-lo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Operationalizing Your R Code](../../advanced-analytics/r/operationalizing-your-r-code.md).

Normalmente, o processo de implantação começa com a limpeza do seu script para eliminar códigos desnecessários na produção. À medida que você move as computações mais para perto dos dados, pode encontrar maneiras de mover, resumir ou apresentar dados com mais eficiência do que fazer tudo no R. Recomendamos que o cientista de dados consulte um desenvolvedor de banco de dados sobre maneiras de melhorar o desempenho, especialmente se a solução faz limpeza de dados ou engenharia de recursos que possa ser mais eficiente no SQL. Podem ser necessárias alterações nos processos de ETL para garantir que os fluxos de trabalho de criação ou pontuação de modelos não falhem e para que os dados de entrada estejam disponíveis no formato correto.

## <a name="see-also"></a>Consulte Também

[Comparação de funções Base R e RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r)

[Biblioteca do RevoScaleR no SQL Server](ref-r-revoscaler.md)
