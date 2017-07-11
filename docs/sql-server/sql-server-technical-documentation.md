---
title: "Documentação técnica do SQL Server | Microsoft Docs"
ms.date: 06/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.portal.f1
helpviewer_keywords:
- documentation [SQL Server], home page
- Help [SQL Server]
- SQL Server, documentation
- home page [SQL Server]
- Help [SQL Server], documentation home page
- Books Online [SQL Server], home page
- portal page [SQL Server]
ms.assetid: 674933a8-e423-4d44-a39b-2a997e2c2333
caps.latest.revision: 106
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: aad94f116c1a8b668c9a218b32372424897a8b4a
ms.openlocfilehash: 334c3d130a1d0c8371c1a7810d82d443e1fbecc8
ms.contentlocale: pt-br
ms.lasthandoff: 06/28/2017

---
<a id="sql-server-technical-documentation" class="xliff"></a>

# Documentação Técnica do SQL Server
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 > Para conteúdo relacionado a versões anteriores do SQL Server, consulte [instalação para SQL Server 2014](https://msdn.microsoft.com/en-US/library/bb500469(SQL.120).aspx).

 Documentação para ajudá-lo a instalar, configurar e usar o SQL Server. O conteúdo inclui exemplos de ponta a ponta, exemplos de código e vídeos. Para tópicos de linguagem do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] , confira [Referência de Linguagem](../t-sql/language-reference.md).

Também é possível exibir a documentação do SQL Server offline usando o Help Viewer. Para obter mais informações, consulte [Help Viewer e conteúdo offline para o SQL Server](../release-notes/sql-server-help-installation.md).

**SQL Server de 2017**

- [Notas de versão do SQL Server de 2017](../sql-server/sql-server-2017-release-notes.md)
- [O que há de novo no SQL Server de 2017](../sql-server/what-s-new-in-sql-server-2017.md)
 
**SQL Server 2016:**
 
- [Notas de Versão do SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
- [Novidades no SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)
    
 **Experimente o SQL Server!**    
 - [**Baixar o SQL Server 2016 do Centro de Avaliação**](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) 
 - **[Crie uma Máquina Virtual com o SQL Server 2016 já instalado](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)**    
 - **[Baixe a versão mais recente do SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)**   
      
<a id="sql-server-technologies" class="xliff"></a>

## Tecnologias do SQL Server    
    
|||    
|-|-|    
|![Mecanismo do Banco de Dados SQL](../sql-server/media/sql-database-engine.png "Mecanismo do Banco de Dados SQL")|**[Mecanismo de Banco de Dados](../database-engine/configure-windows/sql-server-database-engine.md)**<br /><br /> O Mecanismo de Banco de Dados é o serviço principal para armazenamento, processamento e segurança de dados. O Mecanismo de Banco de Dados fornece acesso controlado e processamento rápido de transações para atender aos requisitos dos aplicativos de consumo de dados mais exigentes dentro de sua empresa. O Mecanismo de Banco de Dados também fornece suporte rico para sustentar alta disponibilidade.|    
|![R Server](../sql-server/media/r-server.png "R Server")|**[Serviços R](../advanced-analytics/r-services/r-services.md)**<br /><br /> O Microsoft R Services oferece várias maneiras de incorporar a linguagem R popular nos fluxos de trabalho da empresa.<br /><br /> [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] integra a linguagem R com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], tornando mais fácil criar, treinar novamente e pontuar os modelos chamando os procedimentos armazenados do [!INCLUDE[tsql](../includes/tsql-md.md)] .<br /><br /> O Microsoft R Server fornece suporte multiplataforma e dimensionável para R na empresa e oferece suporte para as fontes de dados, como Hadoop e Teradata.|    
|![Data Quality Services](../sql-server/media/data-quality-services.png "Data Quality Services")|**[Data Quality Services](../data-quality-services/data-quality-services.md)**<br /><br /> O SQL Server Data Quality Services (DQS) fornece uma solução de limpeza de dados controlada por conhecimento. O DQS permite que você crie uma base de dados de conhecimento e use-a para realizar a correção de dados e a eliminação de duplicação de seus dados, usando meios interativos e por computador. Você pode usar serviços de dados de referência baseados em nuvem e criar uma solução de gerenciamento de dados que integra o DQS com o SQL Server Integration Services e o Master Data Services.|    
|![Integration Services](../sql-server/media/integration-services.png "Integration Services")|**[Integration Services](../integration-services/sql-server-integration-services.md)**<br /><br /> [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é uma plataforma para construir soluções para integração de dados de alto desempenho, inclui também pacotes que fornecem processamento de extração, transformação, e carregamento (ETL) para armazenamento de dados.|    
|![Master Data Services](../sql-server/media/master-data-services.png)|**[Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md)**<br /><br /> [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] é a solução do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para gerenciamento de dados mestre. Uma solução criada no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ajuda a assegurar que o relatório e a análise sejam baseados nas informações corretas. Usando o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você cria um repositório central para seus dados mestres e mantém um registro auditável e seguro desses dados conforme eles forem alterados com o tempo.|    
|![Analysis Services](../sql-server/media/analysis-services.png "Analysis Services")|**[Analysis Services](../analysis-services/analysis-services.md)**<br /><br /> O[!INCLUDE[ssASnoversion_md](../includes/ssasnoversion-md.md)] é uma plataforma de dados analíticos e um conjunto de ferramentas para pessoal, equipe e business intelligence corporativo. Os servidores e designers de cliente dão suporte a soluções OLAP tradicionais, novas soluções de modelagem de tabela, bem como análises de autoatendimento e colaboração por meio do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)], o Excel e um ambiente do SharePoint Server. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] também inclui Mineração de Dados para que você possa descobrir os padrões e as relações ocultas dentro de grandes volumes de dados.|    
|![Serviços de replicação](../sql-server/media/replication-services.png "Serviços de replicação")|**[Replicação](../relational-databases/replication/sql-server-replication.md)**<br /><br /> A replicação é um conjunto de tecnologias para copiar e distribuir dados e objetos de um banco de dados para outro e, em seguida, sincronizar entre os bancos de dados para manter a consistência. Ao usar a replicação, é possível distribuir dados para diferentes locais e para usuários remotos e móveis através de redes locais e de longa distância, conexões discadas, conexões sem-fio e a Internet.|    
|![Reporting Services](../sql-server/media/reporting-services.png "Reporting Services")|**[Reporting Services](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)**<br /><br /> O Reporting Services fornece às corporações a funcionalidade de relatórios online possibilitando criar relatórios que se conectam a conteúdos de várias fontes de dados, permite também, publicar os relatórios em diversos formatos e além disso centralizar o gerenciamento de segurança e de assinaturas.|    

    
<a id="earlier-sql-server-versions" class="xliff"></a>

## Versões anteriores do SQL Server
- [Manuais Online para Manuais Online do SQL Server 2014](https://msdn.microsoft.com/library/ms130214(v=sql.120).aspx)
- [Instalar o SQL Server e SQL Server 2014 Express e outras versões mais antigas](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx). (**Obrigado a [Scott Hanselman](http://www.hanselman.com/) para coletar todos os links de pacote do instalador em um único lugar!**)  
- [Documentação técnica do SQL Server 2012](https://technet.microsoft.com/library/bb418433(v=sql.10).aspx)  
- [Documentação do produto do SQL Server 2008 R2](https://msdn.microsoft.com/library/hh278298(v=sql.10).aspx)  
- [Documentação técnica do SQL Server 2008](https://msdn.microsoft.com/library/hh994727(v=sql.10).aspx) 
- [Documentação arquivada do SQL Server 2005](https://msdn.microsoft.com/library/hh278313(v=sql.10).aspx)    

**Bancos de dados de exemplo**  
- [Banco de dados de exemplo do Wide World Importers](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx)  
- [Bancos de dados e scripts de exemplo do AdventureWorks para SQL Server 2016](https://www.microsoft.com/en-us/download/details.aspx?id=49502) 
- [Exemplos de SQL Server no GitHub](https://github.com/Microsoft/sql-server-samples) 
   
<a id="more-information" class="xliff"></a>

 ## Mais informações   
+ [SQL Server Configuration Manager](../relational-databases/sql-server-configuration-manager.md)
+ [Centro de Atualização do SQL Server](https://msdn.microsoft.com/library/ff803383.aspx) links e informações para todas as versões com suporte 
+ [Instalar o Mecanismo de Banco de Dados do SQL Server](../database-engine/install-windows/install-sql-server-database-engine.md) 
+ [Instalar as Ferramentas de Gerenciamento do SQL Server com SSMS](https://msdn.microsoft.com/library/bb500441.aspx) 
+ [SQL Server Data Tools no Visual Studio 2015](https://msdn.microsoft.com/mt186501.aspx)
+ [Vídeos, amostras e recursos da comunidade](https://msdn.microsoft.com/library/dn237258.aspx)
  
[!INCLUDE[feedback_stackoverflow_msdn_connect-md](../includes/feedback-stackoverflow-msdn-connect-md.md)]

