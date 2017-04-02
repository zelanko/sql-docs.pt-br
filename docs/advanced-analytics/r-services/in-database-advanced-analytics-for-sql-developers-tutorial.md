---
title: "An&#225;lise avan&#231;ada no banco de dados para desenvolvedores do SQL (Tutorial) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
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
  - "TSQL"
ms.assetid: c18cb249-2146-41b7-8821-3a20c5d7a690
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# An&#225;lise avan&#231;ada no banco de dados para desenvolvedores do SQL (Tutorial)
O objetivo deste passo a passo é fornecer aos programadores de SQL uma experiência prática na criação de uma solução de análise avançada usando o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Neste passo a passo, você aprenderá a incorporar o R em um aplicativo ou em uma solução de BI encapsulando o código do R em procedimentos armazenados.  
  
## Visão geral  
O processo de criação de uma solução de ponta a ponta normalmente consiste na obtenção e limpeza de dados, exploração de dados e engenharia de recursos, treinamento do modelo e ajuste e, por fim, na implantação do modelo em produção. O desenvolvimento e teste do código do R real serão mais bem executados usando um ambiente de desenvolvimento criado para o R, como RStudio ou [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]. No entanto, depois que a solução for criada, você poderá implantá-la com facilidade no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando os procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] no ambiente conhecido do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
Portanto, neste passo a passo, vamos pressupor que você tenha recebido todo o código do R necessário para a solução, e você vai se concentrar em criar e implantar uma solução analítica avançada já codificada em R.  
  
-   [Etapa 1: Baixar os dados de exemplo](../../advanced-analytics/r-services/step-1-download-the-sample-data-in-database-advanced-analytics-tutorial.md).    Baixe o conjunto de dados de exemplo e os arquivos do script SQL de exemplo em um computador local.  
  
-   [Etapa 2: Importar dados para o SQL Server usando o PowerShell](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md).  Executar um script do PowerShell que cria um banco de dados e uma tabela na instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e que carrega os dados de exemplo na tabela.  
  
-   [Etapa 3: Explorar e visualizar os dados](../../advanced-analytics/r-services/step-3-explore-and-visualize-the-data-in-database-advanced-analytics-tutorial.md).   Realize a exploração e visualização de dados básicos chamando pacotes e funções do R em procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   [Etapa 4: Criar recursos de dados usando o T-SQL](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md).  Crie novos recursos de dados usando funções personalizadas do SQL.  
  
-   [Etapa 5: Treinar e salvar um modelo usando o T-SQL](../../advanced-analytics/r-services/step-5-train-and-save-a-model-using-t-sql.md).  Crie e salve o modelo de aprendizado de máquina usando procedimentos armazenados.  
  
-   [Etapa 6: Colocar o modelo em operação](../../advanced-analytics/r-services/step-6-operationalize-the-model-in-database-advanced-analytics-tutorial.md).  Depois que o modelo for salvo no banco de dados, chame o modelo de previsão no [!INCLUDE[tsql](../../includes/tsql-md.md)] usando procedimentos armazenados.  
  
> [!NOTE]  
> Recomendamos não usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para gravar ou testar o código do R. Se o código do R inserido em um procedimento armazenado apresentar problemas, as informações retornadas pelo procedimento armazenado geralmente serão inadequadas para entender a causa do erro.   
>   
> Para depuração, recomendamos o uso de uma ferramenta como RStudio ou [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]. Os scripts do R fornecidos neste tutorial já foram desenvolvidos e depurados com ferramentas tradicionais do R.  
>   
> Se estiver interessado em aprender a desenvolver scripts do R que podem ser executados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], consulte este tutorial: [Passo a passo de ponta a ponta sobre a ciência de dados](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md))  
  
### Cenário  
Esse passo a passo usa o conjunto de dados conhecido NYC Taxi. Este conjunto de dados público contém 20 GB de arquivos CSV compactados (cerca de 48 GB descompactados), que descrevem os detalhes de mais de 173 milhões de corridas de táxi individuais em 2013, bem como a tarifa paga por cada corrida. Para tornar esse passo a passo rápido e fácil, criamos uma amostragem representativa dos dados: % 1 dos dados, ou 1.703.957 linhas e 23 colunas. Para esse passo a passo, você usará esses dados para criar um modelo de classificação binária que prevê se há probabilidade de uma corrida específica receber uma gorjeta, com base em colunas, como hora do dia, distância e local de embarque de passageiros.  
  
  
### Requisitos  
Esse passo a passo é destinado a usuários já familiarizados com operações de banco de dados fundamentais, como criação de tabelas e bancos de dados, importação de dados em tabelas e criação de consultas SQL. Todo o código do R é fornecido e, portanto, não é necessário nenhum ambiente de desenvolvimento do R. Um programador experiente do SQL deve conseguir concluir esse passo a passo usando o [!INCLUDE[tsql](../../includes/tsql-md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou executando os scripts do PowerShell fornecidos.  
  
No entanto, antes de iniciar o passo a passo, você deve concluir essas preparações:  
  
-   Conecte-se a uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] com o SQL Server R Services habilitado (exige o CTP 3 ou posterior). Para obter detalhes, consulte as instruções de instalação: [Configurar o SQL Server R Services (no banco de dados)](https://msdn.microsoft.com/library/mt696069.aspx)  
  
 -   O logon usado para este passo a passo deve ter permissões para criar bancos de dados e outros objetos, carregar dados, selecionar dados e executar procedimentos armazenados.  
  
## Próxima etapa  
[Etapa 1: Baixar os dados de exemplo](../../advanced-analytics/r-services/step-1-download-the-sample-data-in-database-advanced-analytics-tutorial.md)  
  
## Consulte também  
[Tutoriais do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
[SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  
  
