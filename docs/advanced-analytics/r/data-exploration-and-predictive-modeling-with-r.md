---
title: "Exploração e Dados e Modelagem Preditiva com R | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bf6de7e2-f394-4b8a-a4b7-0b8dadf25426
caps.latest.revision: "20"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 79f82cbf4cba40a4c4fd2b2683ce3c16913ef315
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="data-exploration-and-predictive-modeling-with-r"></a>Exploração e Dados e Modelagem Preditiva com R

Este tópico descreve os aprimoramentos para o processo de ciência de dados que são possíveis por meio da integração com o SQL Server.

Aplica-se a: SQL Server 2016 R Services, serviços de Learnign de máquina do SQL Server de 2017

## <a name="the-data-science-process"></a>O processo de ciência de dados

Cientistas de dados geralmente usam R para explorar dados e criar modelos preditivos. Esse geralmente é um processo iterativo de tentativa e erro até chegar a um bom modelo preditivo. Com um cientista de dados experiente, você pode se conectar ao banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e buscar os dados para sua estação de trabalho local usando o pacote RODBC, explorar seus dados e criar um modelo preditivo usando pacotes R padrão.

No entanto, essa abordagem tem várias desvantagens, que hae prejudicada a mais ampla adoção de R na empresa. 

+ Movimentação de dados pode ser ineficiente, insegura ou lenta
+ R em si tem limitações de desempenho e escalabilidade

Essas desvantagens se tornam mais aparentes quando você precisa mover e analisar grandes quantidades de dados ou usar conjuntos de dados que não cabem na memória disponível em seu computador.

Os pacotes de novo, escalonáveis e funções R incluídas com [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ajudá-lo a superar muitos desses desafios. 

## <a name="whats-different-about-revoscaler"></a>O que é diferente RevoScaleR?

O pacote **RevoScaleR** contém implementações de algumas das funções R mais populares, que foram remodeladas para oferecer paralelismo e escalabilidade. Para obter mais informações, consulte [Distributed Computing usando o RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing).

O pacote RevoScaleR também oferece suporte para alteração do *contexto de execução*. Isso significa que, para uma solução inteira ou apenas uma função, você pode indicar que computações devem ser realizadas usando os recursos do computador que hospeda a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em vez de sua estação de trabalho local. Essa abordagem tem diversas vantagens: você evita a movimentação desnecessária de dados e pode aproveitar mais recursos de computação no computador do servidor.

## <a name="r-environment-and-packages"></a>Pacotes e Ambiente R

O ambiente de R com suporte no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] consiste em um tempo de execução, a linguagem de código aberto e um mecanismo gráfico com suporte e estendido por vários pacotes. A linguagem permite uma variedade de extensões que são implementadas usando pacotes.  

### <a name="using-other-r-packages"></a>O uso de outros pacotes de R

Além das bibliotecas de R proprietárias incluídas no aprendizado de máquina do Microsoft, você pode usar quase todos os pacotes de R em sua solução, incluindo:

+ Pacotes de R de finalidade geral de repositórios públicos. Você pode obter os pacotes R de código aberto de repositórios públicos populares, como o CRAN, que hospeda mais 6000 pacotes que podem ser usados por cientistas de dados.
  
  Para a plataforma Windows, os pacotes de R são fornecidos como arquivos zip e podem ser baixados e instalados sob a licença GPL.  
  
  Para saber mais sobre como instalar pacotes de terceiros para usar com o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], veja [Install Additional R Packages on SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
  
+ Pacotes e bibliotecas adicionais fornecidos pelo [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].   
  
     O pacote **RevoScaleR** inclui análise de alto desempenho de Big Data, versões aprimoradas de funções que dão suporte a tarefas comuns de ciência de dados, aprendizes otimizados para Naive Bayes, regressão linear, modelos de série temporal e redes neurais e bibliotecas matemáticas avançadas.  
  
     O pacote **RevoPemaR** permite que você desenvolva seus próprios algoritmos de memória externa paralela em R.  
  
     Para obter mais informações sobre esses pacotes e como usá-los, consulte [novidades RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) e [Introdução ao RevoPemaR](https://msdn.microsoft.com/microsoft-r/pemar-getting-started). 

+ **MicrosoftML** contém uma coleção de algoritmos de aprendizado de máquina altamente otimizada e transformações de dados da equipe de ciência de dados da Microsoft. Muitos dos algoritmos também são usados no aprendizado de máquina do Azure. Para obter mais informações, consulte [usando o pacote MicrosoftML](../../advanced-analytics/using-the-microsoftml-package.md).

### <a name="r-development-tools"></a>Ferramentas de Desenvolvimento R

Ao desenvolver sua solução R, certifique-se de baixar o cliente do Microsoft R. Este download gratuito inclui as bibliotecas necessárias para oferecer suporte a contextos de computação remoto e escalonável alorithms:

+ **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]:** uma distribuição do tempo de execução R e um conjunto de pacotes, como a biblioteca de kernel de matemática da Intel, que melhora o desempenho de operações R padrão.  
  
+ **RevoScaleR:** um pacote de R que lhe permite enviar computações por push a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]. Ele também inclui um conjunto de funções R comuns que foram reprojetadas para fornecer melhor desempenho e escalabilidade. Você pode identificar essas funções aprimoradas pelo prefixo **rx** . Ele também inclui provedores de dados aprimorados para uma variedade de fontes; essas funções são prefixadas com **Rx**.

Você pode usar qualquer editor de código baseado em Windows que oferece suporte a R, como [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] ou RStudio. O download do [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] também inclui ferramentas de linha de comando comuns para R, como RGui.exe.

## <a name="use-new-data-sources-and-compute-contexts"></a>Use novas fontes de dados e contextos de computação

Ao usar o pacote RevoScaleR para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], procure por essas funções para usar em seu código R:

+ **RxSqlServerData** é uma função fornecida no pacote RevoScaleR para oferecer suporte à conectividade de dados aprimorada com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
     Use essa função em seu código R para definir a *fonte de dados*. O objeto da fonte de dados especifica o servidor e as tabelas onde os dados residem e gerencia a tarefa de ler e gravar dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
-   O pacote **RxInSqlServer** pode ser usada para especificar o *contexto de computação*.  Em outras palavras, você pode indicar onde o código R deve ser executado: na sua estação de trabalho local ou no computador que hospeda a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  Para obter mais informações, consulte [funções de RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler).
  
     Quando você define o contexto de computação, ele afeta somente os cálculos que dão suporte ao contexto de execução remota, o que significa as operações R fornecidas pelo pacote RevoScaleR e funções relacionadas. Normalmente, as soluções de R com base em pacotes CRAN padrão não podem ser executadas em um contexto de computação remota, embora possam ser executadas no computador [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] se iniciadas pelo T-SQL. No entanto, é possível usar a função `rxExec` para chamar funções de R individuais e executá-las remotamente em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

Para obter exemplos de como criar e trabalhar com fontes de dados e contextos de execução, consulte estes tutoriais:

+ [Aprofundamento da ciência de dados](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)  
+  [Análise de dados usando o Microsoft R](https://msdn.microsoft.com/en-us/microsoft-r/data-analysis-in-microsoft-r)

## <a name="deploy-r-code-to-production"></a>Implantar o código R em produção

Uma parte importante da ciência de dados é fornecer suas análises para outras pessoas ou usar modelos preditivos para melhorar os resultados ou processos de negócios. No [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], é fácil passar para a produção quando seu script ou modelo R estiver pronto.

Para saber mais sobre como mover seu código para executá-lo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Operationalizing Your R Code](../../advanced-analytics/r/operationalizing-your-r-code.md).

Normalmente, o processo de implantação começa com a limpeza do seu script para eliminar códigos desnecessários na produção. Como mover cálculos mais próximo para os dados, você pode encontrar formas de com mais eficiência mover, resumir ou apresentar dados do que fazer tudo no R.  É recomendável que o cientista de dados Consulte com um desenvolvedor de banco de dados sobre maneiras de melhorar o desempenho, especialmente se a solução não limpeza de dados ou o recurso de engenharia que pode ser mais eficaz em SQL. Podem ser necessárias alterações nos processos de ETL para garantir que os fluxos de trabalho de criação ou pontuação de modelos não falhem e para que os dados de entrada estejam disponíveis no formato correto.

## <a name="see-also"></a>Consulte também

[Comparação de funções Base R e ScaleR](https://msdn.microsoft.com/microsoft-r/scaler/compare-base-r-scaler-functions)

[Funções ScaleR para trabalhar com o SQL Server](../../advanced-analytics/r/scaler-functions-for-working-with-sql-server-data.md)
