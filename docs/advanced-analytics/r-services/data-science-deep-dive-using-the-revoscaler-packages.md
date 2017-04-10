---
title: "Aprofundamento da ci&#234;ncia de dados: Usando os pacotes RevoScaleR | Microsoft Docs"
ms.custom: ""
ms.date: "09/27/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: c2efb3f2-cad5-4188-b889-15d68b742ef5
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# Aprofundamento da ci&#234;ncia de dados: Usando os pacotes RevoScaleR
Este tutorial é uma introdução aos pacotes do R avançados fornecidos no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Você aprenderá como usar a estrutura corporativa escalonável para a execução de pacotes do R no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].   Usando essas funções do R escaláveis, um cientista de dados pode criar soluções personalizadas do R executadas em contextos local ou do servidor, a fim de dar suporte à análise de Big Data de alto desempenho.  
  
Neste tutorial, você aprenderá como mover dados entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e sua estação de trabalho do R, analisar e plotar os dados e criar e implantar modelos.  
    
## Visão geral 
 
Para ilustrar o poder de processamento e a flexibilidade dos pacotes ScaleR, neste tutorial, você moverá dados e trocará contextos de computação com frequência.

+ Inicialmente, os dados são obtidos dos arquivos CSV ou XDF. Você importará os dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando as funções no pacote RevoScaleR.    
+ O treinamento e a pontuação do modelo serão executadas no contexto de computação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
    Você criará novas tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], usando as funções **rx**, para salvar os resultados da pontuação.    
+ Você criará plotagens tanto no servidor quanto no contexto de computação local.  
+ Para treinar o modelo, você usará os dados já armazenados em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Todos os cálculos serão executados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
+ Você extrairá um subconjunto de dados e os salvará como um arquivo XDF para usá-los novamente em análises em sua estação de trabalho local.    
+ Os novos dados usados durante o processo de pontuação são extraídos do banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de uma conexão ODBC. Todos os cálculos são executados na estação de trabalho local. 
+ Por fim, você executará uma simulação com base em uma função do R personalizada usando o contexto de computação do servidor.

### Comece agora mesmo  

Este tutorial leva cerca de uma hora para ser concluído, não incluindo a instalação.  

-   [Lição 1: Trabalhar com dados do SQL Server usando o R](../../advanced-analytics/r-services/lesson-1-work-with-sql-server-data-using-r-data-science-deep-dive.md)  
  
-   [Lição 2: Criar e executar scripts do R](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
-   [Lição 3: Transformar dados usando o R](../../advanced-analytics/r-services/lesson-3-transform-data-using-r-data-science-deep-dive.md)  
  
-   [Lição 4: Analisar dados no contexto de computação local](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md)  
  
-   [Lição 5: Criar uma simulação simples](../../advanced-analytics/r-services/lesson-5-create-a-simple-simulation-data-science-deep-dive.md)  

      
### Público-alvo  
  
Este tutorial destina-se a cientistas de dados ou a pessoas que já estejam minimamente familiarizadas em tarefas de ciência de dados e do R, incluindo exploração, análise estatística e ajuste de modelos.  No entanto, todo o código é fornecido. Portanto, você pode executar o código facilmente e acompanhá-lo, supondo que você tenha os ambientes de cliente e de servidor necessários.  
  
Você também deve estar familiarizado com a sintaxe do [!INCLUDE[tsql](../../includes/tsql-md.md)] e saber como acessar um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou outras ferramentas de banco de dados, como o Visual Studio.  
  
> [!TIP]  
> Salve seu espaço de trabalho do R entre as lições para que você possa facilmente selecionar a seção em que parou.  
  
### Pré-requisitos  
  
-   **Servidor de banco de dados com suporte no R**  
  
    Instale o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e habilite o SQL Server R Services (no banco de dados). Esse processo é descrito em [Manuais Online do SQL Server 2016](http://msdn.microsoft.com/library/mt696069(SQL.130).aspx).  
  
-   **Permissões de banco de dados**  
  
    Para executar as consultas usadas para treinar o modelo, você deve ter privilégios **db_datareader** no banco de dados em que os dados são armazenados.  
  
  
-   **Estação de trabalho de ciência de dados**  
  
    Você deve instalar os pacotes RevoScaleR. A maneira mais fácil de fazer isso é instalar o Microsoft R Server (autônomo) ou o cliente Microsoft R. Para obter mais informações, consulte [Configurar um cliente de ciência de dados](http://msdn.microsoft.co/library/mt696067(SQL.130).aspx)
      
    > [!NOTE] 
    > Não há suporte para outras versões do Revolution R Enterprise ou Revolution R Open. 
    > 
    > Uma distribuição de software livre de R, como R 3.2.2, não funcionará neste tutorial, porque somente a função ScaleR pode usar contextos de computação remota. 
  
-   **Pacotes do R adicionais**  
  
    Para este tutorial, você precisará instalar os seguintes pacotes: **dplyr**, **ggplot2**, **ggthemes**, **reshape2** e **e1071**. Instruções são fornecidas como parte do tutorial.  
  
    Todos os pacotes também devem ser instalados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que o treinamento será executado. É importante que os pacotes sejam instalados na biblioteca de pacotes do R usada pelo SQL Server. **Não instale os pacotes em uma biblioteca do usuário.** Se você não tem permissão para instalar pacotes nessa pasta, solicite ao administrador do banco de dados para adicionar os pacotes.   
  
Para obter mais informações, consulte [Pré-requisitos para o passo a passo da ciência de dados #40;SQL Server R Services&#41;](../../advanced-analytics/r-services/prerequisites-for-data-science-walkthroughs-sql-server-r-services.md).  
  
## Estratégias de dados para soluções de R distribuído
    
Em geral, antes de começar a escrever e executar scripts do R no ambiente de desenvolvimento local, sempre reserve um minuto para planejar o uso de dados e determinar quando executar cada parte da solução para melhor desempenho.  

Neste tutorial, você ganhará experiência com as funções de alto desempenho para analisar dados, criar modelos e plotagens incluídos no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Vamos nos referir a essas funções, em geral, como ScaleR ou Microsoft R, para distingui-las das funções derivadas de outros pacotes R de software livre. Para obter mais informações sobre como o Microsoft R difere do R de software livre, consulte este [Guia de Introdução](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#microsoft-r-products). 

Um benefício importante da utilização de funções ScaleR é que elas dão suporte ao uso de *fontes de dados* locais ou do servidor e de *contextos de computação* local ou remota.  Portanto, à medida que você trabalha neste tutorial, considere as estratégias de dados que talvez você precise adotar para suas próprias soluções.
  
-   **Que tipo de análise você deseja executar?** É algo para seu uso individual ou você vai compartilhar os modelos, resultados ou gráficos com outras pessoas?
 
    Neste tutorial, você aprenderá como movimentar os resultados em seu ambiente de desenvolvimento e o servidor para facilitar o compartilhamento e a análise. 
  
-   **O pacote R de que você precisa dá suporte à execução remota?** Todas as funções nos pacotes ScaleR fornecidos pelo [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] podem ser executadas nos contextos de computação remota e potencialmente usar a execução paralela. Por outro lado, as funções em pacotes de terceiros podem exigir outros recursos para a execução de thread único. 
    
    Neste tutorial, você aprenderá como mudar entre contextos de computação local e remota para usar os recursos de servidor quando necessário. Você também aprenderá como encapsular funções do R padrão em *rxExec* para dar suporte à execução remota de funções do R arbitrárias.
    
  
-   **Em que local estão os dados e quais são suas características?**  Se os dados residirem localmente, você deverá decidir se carregará todos os novos dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou treinará localmente e salvará apenas o modelo no banco de dados. No entanto, quando você implanta em produção, talvez você precise treinar nos dados corporativos e usar processos de ETL para limpar e carregar os dados.  
  
-   Perguntas semelhantes se aplicam a dados de pontuação. Você criará o pipeline de dados para pontuar dados na estação de trabalho ou usará fontes de dados empresariais? A limpeza e preparação de dados devem ser executadas como parte dos processos ETL ou você está executando um experimento único?  

    Neste tutorial, você aprenderá como mover dados de maneira eficiente e segura entre seu ambiente R local e o SQL Server. 
  
-   **Qual contexto de computação você deveria usar?** Treine seu modelo localmente nos dados amostrados e, em seguida, mude para o uso de dados do servidor para teste e produção.

    Neste tutorial, você aprenderá como mover dados entre o SQL Server e o R usando o R. Você também aprenderá como trabalhar com dados usando arquivos XDF e como processar dados em partes usando as funções ScaleR.  
  
 
  
## Próxima etapa  
[Lição 1: Trabalhar com dados do SQL Server usando o R &#40;Aprofundamento da ciência de dados&#41;](../../advanced-analytics/r-services/lesson-1-work-with-sql-server-data-using-r-data-science-deep-dive.md)  
  
  
  
