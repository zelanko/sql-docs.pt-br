---
title: "Explora&#231;&#227;o e Dados e Modelagem Preditiva com R | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bf6de7e2-f394-4b8a-a4b7-0b8dadf25426
caps.latest.revision: 20
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# Explora&#231;&#227;o e Dados e Modelagem Preditiva com R
  Cientistas de dados geralmente usam R para explorar dados e criar modelos preditivos. Esse geralmente é um processo iterativo de tentativa e erro até chegar a um bom modelo preditivo. Com um cientista de dados experiente, você pode se conectar ao banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e buscar os dados para sua estação de trabalho local usando o pacote RODBC, explorar seus dados e criar um modelo preditivo usando pacotes R padrão.  
  
 No entanto, essa abordagem tem desvantagens. A movimentação de dados pode ser ineficiente, insegura ou lenta e o R em si tem limitações de desempenho e escalabilidade. Essas desvantagens se tornam mais aparentes quando você precisa mover e analisar grandes quantidades de dados ou usar conjuntos de dados que não cabem na memória disponível em seu computador.  
  
 Pode superar esses desafios usando os novos pacotes escalonáveis e funções R incluído com [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. O pacote **RevoScaleR** contém implementações de algumas das funções R mais populares, que foram remodeladas para oferecer paralelismo e escalabilidade. O pacote RevoScaleR também oferece suporte para alteração do *contexto de execução*. Isso significa que, para uma solução inteira ou apenas uma função, você pode indicar que computações devem ser realizadas usando os recursos do computador que hospeda a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em vez de sua estação de trabalho local. Essa abordagem tem diversas vantagens: você evita a movimentação desnecessária de dados e pode aproveitar mais recursos de computação no computador do servidor.  
  
 Esta seção fornece orientações para cientistas de dados sobre como usar o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] e realizar tarefas relacionadas ao desenvolver e testar soluções R.  
  
##  <a name="bkmk_RDevTools"></a> Ferramentas de Desenvolvimento R  
 R o cliente do Microsoft oferece um ambiente completo de desenvolvimento e teste de modelos de previsão de cientista de dados. R cliente inclui:  
  
-  **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]:** Uma distribuição do runtime R e um conjunto de pacotes, como a biblioteca de kernel de matemática Intel, melhorar o desempenho de operações padrão de R.  
  
-   **RevoScaleR:** um pacote R que permite enviar por push computações para uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]. Ele também inclui um conjunto de funções comuns de R que foram reprojetadas para fornecer um melhor desempenho e escalabilidade. Você pode identificar essas funções aprimoradas pelo prefixo **rx** . Ele também inclui provedores de dados avançada para uma variedade de fontes. Essas funções são prefixadas com **Rx**.  
  
-   **Libere a variedade de ferramentas de desenvolvimento:** você pode usar qualquer editor de códigos baseados no Windows que oferece suporte a R, como [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] ou RStudio. O download do [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] também inclui ferramentas de linha de comando comuns para R como RGui.exe.  
  
##  <a name="bkmk_packages"></a> Pacotes e Ambiente R  
 O ambiente de R com suporte no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] consiste em um tempo de execução, a linguagem de código aberto e um mecanismo gráfico com suporte e estendido por vários pacotes. A linguagem permite uma variedade de extensões que são implementadas usando pacotes.  
  
 Há várias fontes de pacotes R adicionais que você pode usar com o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] :  
  
  
-   Pacotes de R de finalidade geral de repositórios públicos. Você pode obter os pacotes R de código aberto de repositórios públicos populares, como o CRAN, que hospeda mais 6000 pacotes que podem ser usados por cientistas de dados.  
  
     Pacotes adicionais são disponibilizados para oferecer suporte à análise preditiva em domínios especiais, como finanças, genômica e assim por diante.  
  
     Para a plataforma Windows, pacotes R são fornecidos como arquivos zip e podem ser baixados e instalados sob a licença GPL.  
  
     Para obter informações sobre como instalar pacotes de terceiros para uso com [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], consulte [instalar pacotes de R adicionais no SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
-   Pacotes adicionais e bibliotecas fornecido pelo [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].   
  
     O **RevoScaleR** pacote inclui análise de grandes volumes de dados de alto desempenho, versões aprimoradas de funções que oferecem suporte a tarefas de ciência de dados comuns, aprendizes otimizados para Bayesiana, regressão linear, modelos de série temporal e redes neurais e bibliotecas matemáticas avançadas.  
  
     O pacote **RevoPemaR** permite que você desenvolva seus próprios algoritmos de memória externa paralela em R.  
  
     Para obter mais informações sobre esses pacotes e como usá-los, consulte [exploração de dados e modelagem de previsão e 40; Tutorial: Serviços do SQL Server R & 41;](../../advanced-analytics/r-services/sql-server-r-services.md).  
  
## Usar Fontes de Dados e Contextos de Computação  
 Ao usar o pacote de RevoScaleR para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], existem algumas novas funções importantes para usar em seu código R:  
  
-   [RxSqlServerData](RxSqlServerData.md) é uma função fornecida no pacote RevoScaleR para oferecer suporte à conectividade de dados aprimorada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Use essa função em seu código R para definir a *fonte de dados*. O objeto da fonte de dados especifica o servidor e as tabelas onde os dados residem e gerencia a tarefa de ler e gravar dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   O [RxInSqlServer](rxInSqlServer.md) função pode ser usada para especificar o *computação contexto*.  Em outras palavras, você pode indicar onde o código R deve ser executado: na sua estação de trabalho local ou no computador que hospeda o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.  
  
     Quando você define o contexto de computação, ele afeta somente computações que oferecem suporte a contexto de execução remota, o que significa que operações de R fornecido pelo pacote RevoScaleR e funções relacionadas. Normalmente, soluções de R com base em pacotes CRAN padrão não podem ser executado em um contexto de computação remota, embora possam ser executados [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] computador se iniciado por T-SQL. No entanto, você pode usar o `rxExec` função para chamar funções de R individuais e executá-los remotamente em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  
  
 Para obter exemplos de como criar e trabalhar com fontes de dados e contextos de execução, consulte os tutoriais:
 
 + [Aprofundamento de ciência de dados](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
 +  [Servidor SQL RevoScaleR Introdução](https://msdn.microsoft.com/microsoft-r/rserver/rserver-scaler-sql-server-getting-started).  
  
## Implantar seu Código R em Produção  
 Uma parte importante da ciência de dados é fornecer suas análises para outras pessoas ou usar modelos preditivos para melhorar os resultados ou processos de negócios. No [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], é fácil passar para a produção quando seu script ou modelo R estiver pronto.  
  
 Para obter mais informações sobre como você pode mover seu código seja executado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [operacionalização seu código R](../../advanced-analytics/r-services/operationalizing-your-r-code.md).  
  
 Normalmente, o processo de implantação começa com a limpeza do seu script para eliminar códigos desnecessários na produção. como mover computações mais próximo para os dados, você pode encontrar maneiras de mover com mais eficiência, resumir ou apresentar dados em vez de fazer tudo em R.  
  
 É recomendável que consulte o cientista de dados com um desenvolvedor de banco de dados sobre as maneiras de melhorar o desempenho, especialmente se a solução não limpeza de dados ou o recurso de engenharia que pode ser mais eficiente no SQL. Alterações nos processos de ETL deve ser necessária para garantir que os fluxos de trabalho de criação ou um modelo de pontuação não falham, e que os dados de entrada estão disponíveis no formato correto.  
  
##  <a name="bkmk_SQLInR"></a> Nesta seção  

[Comparação de funções de ScaleR e CRAN R](Summary%20of%20rx%20Functions.md)

[Funções de scaleR para trabalhar com o SQL Server](../../advanced-analytics/r-services/scaler-functions-for-working-with-sql-server-data.md)
   
## Consulte também  

 
 [Recursos e tarefas do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)   
 
 [Operacionalização do Código R](../../advanced-analytics/r-services/operationalizing-your-r-code.md)  
  
  