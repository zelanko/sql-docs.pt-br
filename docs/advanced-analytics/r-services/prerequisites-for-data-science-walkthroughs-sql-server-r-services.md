---
title: "Pr&#233;-requisitos para o passo a passo da ci&#234;ncia de dados (SQL Server R Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/22/2016"
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
ms.assetid: 0b0582b8-8843-4787-94a8-2e28bdc04fb2
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# Pr&#233;-requisitos para o passo a passo da ci&#234;ncia de dados (SQL Server R Services)
Recomendamos que você siga o passo a passo em uma estação de trabalho do R que pode se conectar a um computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na mesma rede. Você também pode executar o passo a passo em um computador que tem o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o ambiente de desenvolvimento do R. 
  
  
## <a name="install-sql-server-2016-r-services-in-database"></a>Instalar o SQL Server 2016 R Services (no banco de dados)  
Você deve ter acesso a uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  com o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] instalado. Para obter mais informações sobre como configurar o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], consulte [Configurar o SQL Server R Services (no banco de dados](https://msdn.microsoft.com/library/mt696069.aspx).  
  
  
> [!IMPORTANT]  
> Use o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ou posterior. As versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dão suporte à integração com o R. Entretanto, você pode usar bancos de dados SQL como uma fonte de dados ODBC.  
  
## <a name="install-an-r-development-environment"></a>Instalar um ambiente de desenvolvimento do R  
Para concluir este passo a passo no computador, você precisará de um ambiente de desenvolvimento do R ou de outra ferramenta de linha de comando que pode executar comandos do R.    
  
- **R Tools para Visual Studio** é um plug-in gratuito que fornece o Intellisense, depuração e suporte para o Microsoft R Server e o SQL Server R Services. Para baixar, consulte [R Tools para Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx).  
    
- O **cliente do Microsoft R** é uma ferramenta de desenvolvimento leve que oferece suporte ao desenvolvimento em R usando os pacotes ScaleR. Para fazer isso, veja [Começar a usar o cliente do Microsoft R](https://msdn.microsoft.com/microsoft-r/r-client-get-started).
  
- O**RStudio** é um dos ambientes mais populares para desenvolvimento do R. Para obter mais informações, visite [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/).  
  
    Entretanto, não é possível concluir este tutorial usando uma instalação genérica do RStudio ou em outro ambiente; você também deve instalar os pacotes do R e as bibliotecas de conectividade do Microsoft R Open. Para obter mais informações, consulte [Configurar um cliente de ciência de dados](https://msdn.microsoft.com/library/mt696067.aspx).  

- Ferramentas do R (R.exe, RTerm.exe, RScripts.exe) são instaladas por padrão quando você instala o [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]. Se você não desejar instalar um IDE, poderá usar essas ferramentas.  
  
  
## <a name="get-permissions-to-connect-to-sql-server"></a>Obter permissões para se conectar ao SQL Server  
Neste passo a passo, você se conectará a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar scripts e carregar dados. Para fazer isso, é necessário ter um logon válido no servidor de banco de dados.  Você pode usar um logon SQL ou a autenticação integrada do Windows. Peça ao administrador de banco de dados para criar uma conta para você no servidor com esses privilégios no banco de dados em que você usará o R:  
  
-   Criar banco de dados, tabelas, funções e procedimentos armazenados    
-   Inserir dados em tabelas  
  
  
## <a name="start-the-walkthrough"></a>Iniciar o passo a passo  
[Lição 1: Preparar os dados &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
