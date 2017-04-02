---
title: "Criando fluxos de trabalho que usam R no SQL Server | Microsoft Docs"
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
ms.assetid: 34c3b1c2-97db-4cea-b287-c7f4fe4ecc1b
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Criando fluxos de trabalho que usam R no SQL Server
  Um banco de dados relacional é uma tecnologia altamente otimizada para fornecer soluções escalonáveis para processamento, armazenamento e consulta de dados de transações. No entanto, tradicionalmente soluções R têm geralmente dependia importando dados de várias fontes, geralmente no formato CSV, para executar a modelagem e exploração de dados adicional. Essas práticas não são apenas ineficientes, mas inseguras.  
  
 Usando [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] oferece várias vantagens:  
  
-   Segurança de dados. O poder de R é colocado no banco de dados, mais próximo à fonte de dados. Evita a movimentação de dados de um desperdício ou insegura.  
  
-   Velocidade. Bancos de dados são otimizados para operações baseadas em conjunto. Além disso, as recentes inovações em bancos de dados, como tabelas na memória e armazenamento de dados Colunar mais melhorar o ciência de dados fazendo agregações muito mais velozes.  
  
-   Integração. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é o ponto central de operações para muitas outras tarefas de gerenciamento de dados e aplicativos que consomem enterprise. Usando dados já no banco de dados garante que os dados são consistentes e atualizadas. Em vez de processar dados em R, você pode contar com pipelines de dados corporativos incluindo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e Azure Data Factory. Relatório de resultados ou análises é fácil por meio do Power BI ou [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Usando a combinação certa de SQL e R para processamento de dados e tarefas analíticas diferentes, desenvolvedores e cientistas de dados podem ser mais produtivos. Esta seção descreve como você pode integrar o R com outras soluções empresariais para transformação de dados, análise e relatórios.  
  
##  <a name="bkmk_ssis"></a> Criar fluxos de trabalho eficientes que abrangem R e o banco de dados  
 Fluxos de trabalho de ciência de dados são altamente iterativos e envolvem muita transformação de dados, incluindo dimensionamento, agregações, cálculo de probabilidades, renomeação e mesclagem de atributos. Cientistas de dados estão acostumados a fazer muitas dessas tarefas em R, Python ou outra linguagem; No entanto, esses fluxos de trabalho em execução nos dados da empresa requer integração com processos e ferramentas ETL.  
  
 Porque [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] permite que você execute operações complexas em R por meio do Transact-SQL e procedimentos armazenados, você pode integrar tarefas específicas de R com processos de ETL existentes sem o trabalho de desenvolvimento de novo mínimo. Em vez de executar uma cadeia de memória ntensive tarefas em R, preparação de dados pode ser otimizada usando as ferramentas mais eficientes, incluindo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Por exemplo, você pode combinar R com [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em cenários como estes:  
  
-   Use [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tarefas para criar os objetos necessários no banco de dados SQL  
  
-   Usar ramificação condicional para alternar o contexto de computação para trabalhos em R  
  
-   Executar trabalhos em R que geram seus próprios dados  
  
-   Usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para chamar um script R salvo em uma variável de texto  
  
### Exemplos e recursos  
 [Colocar em operação o seu projeto de aprendizado de máquina usando o SQL Server 2016 SSIS e serviços de R](https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/)  
  
 Nesta postagem de blog, você aprenderá como:  
  
-   Usar R na tarefa Executar SQL para gerar dados e salvá-lo em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Use um procedimento armazenado para treinar um modelo de R e armazená-lo no banco de dados  
  
-   Executar o modelo usando a tarefa de Script e a tarefa Executar SQL de pontuação  
  
##  <a name="bkmk_ssrs"></a> Criar visualizações que abrangem R e ferramentas de relatório empresariais  
 Embora R possa criar gráficos e efeitos visuais interessantes, não é bem integrado com fontes de dados externas, significando que cada de gráfico tem de ser produzido individualmente. Compartilhamento também pode ser difícil.  
  
 Usando [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], você pode executar operações complexas em R via [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos armazenados, que podem ser facilmente consumidos por uma variedade de ferramentas, inclusive de relatórios corporativos [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e Power BI.  
  
-   Visualizar objetos gráficos retornados de um script R   
    usando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   Use a tabela no Power BI  
  
## Exemplos e recursos  
 [Dispositivo de gráficos de R para o Microsoft Reporting Services (SSRS)](https://rgraphicsdevice.codeplex.com/)  
  
 Este projeto CodePlex fornece o código para ajudá-lo a criar um item de relatório personalizado que processa a saída de gráficos de R como uma imagem que pode ser usada em [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] relatórios.  Usando o item de relatório personalizado, você pode:  
  
-   Publicar gráficos e gráficos plotados criado usando o dispositivo gráfico R [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] painéis  
  
-   Passar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] parâmetros para gráficos de R  
  
> [!NOTE]  
>  Observe que o código que suporta o dispositivo gráfico R para o Reporting Services deve ser instalado no servidor do Reporting Services, bem como no Visual Studio. Configuração e a compilação manual também é necessária.  
  
  