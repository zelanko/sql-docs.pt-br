---
title: "Documentação do SQL Server | Microsoft Docs"
ms.date: 10/30/2017
ms.prod: sql-server
ms.prod_service: sql-non-specified
ms.service: server-general
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.portal.f1
helpviewer_keywords:
- documentation [SQL Server], home page
- Help [SQL Server]
- SQL Server, documentation
- home page [SQL Server]
- Help [SQL Server], documentation home page
- Books Online [SQL Server], home page
- portal page [SQL Server]
ms.assetid: 674933a8-e423-4d44-a39b-2a997e2c2333
caps.latest.revision: "106"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 83e7ed6db9331c4d5aba05d1df845b7e5f1733df
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="sql-server-documentation"></a>Documentação do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O SQL Server é uma parte central da plataforma de dados Microsoft. O SQL Server é líder do setor em ODBMS (sistemas de gerenciamento de bancos de dados operacionais). Esta documentação ajuda você a instalar, configurar e usar o SQL Server. O conteúdo inclui exemplos de ponta a ponta, exemplos de código e vídeos. Para tópicos de linguagem do SQL Server, consulte a [Referência de linguagem](../t-sql/language-reference.md).

|Novidades  | Notas de versão  |
|---------|---------|
|[Novidades no SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)     | [Notas de Versão do SQL Server 2017.](../sql-server/sql-server-2017-release-notes.md)        |
|[Novidades no SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)     | [Notas de Versão do SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)        |
|[Novidades do SQL Server 2014](https://msdn.microsoft.com/library/bb500435(v=sql.120).aspx)     | [SQL Server 2014 Release Notes](../sql-server/sql-server-2014-release-notes.md)        |
   
**Experimente o SQL Server!**

|||
|-|-|
|[![Baixar no Centro de Avaliação](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=829477) [Baixar o SQL Server 2017](http://go.microsoft.com/fwlink/?LinkID=829477) | [![Baixar no Centro de Avaliação](../includes/media/download2.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) [Baixar o SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) |
|[![Criar uma máquina virtual](../includes/media/azure-vm.png)](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) [Criar uma máquina virtual com o SQL Server](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) | [![Baixar no Centro de Avaliação](../includes/media/download2.png)](../ssms/download-sql-server-management-studio-ssms.md) [Baixar o SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) |
| [![Baixar no Centro de Avaliação](../includes/media/download2.png)](../ssdt/download-sql-server-data-tools-ssdt.md) [Baixar o SSDT (SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md) | |

    
## <a name="sql-server-technologies"></a>Tecnologias do SQL Server    
    
|||    
|-|-|    
|![Mecanismo do Banco de Dados SQL](../sql-server/media/sql-database-engine.png "Mecanismo do Banco de Dados SQL")|**[Mecanismo de Banco de Dados](../database-engine/configure-windows/sql-server-database-engine.md)**<br /><br /> O Mecanismo de Banco de Dados é o serviço principal para armazenamento, processamento e segurança de dados. O Mecanismo de Banco de Dados fornece acesso controlado e processamento rápido de transações para atender aos requisitos dos aplicativos de consumo de dados mais exigentes dentro de sua empresa. O Mecanismo de Banco de Dados também fornece suporte rico para sustentar alta disponibilidade.|
|![Integration Services](../sql-server/media/integration-services.png "Integration Services")|**[Integration Services](../integration-services/sql-server-integration-services.md)**<br /><br /> [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é uma plataforma para construir soluções para integração de dados de alto desempenho, inclui também pacotes que fornecem processamento de extração, transformação, e carregamento (ETL) para armazenamento de dados.|    
|![Analysis Services](../sql-server/media/analysis-services.png "Analysis Services")|**[Analysis Services](../analysis-services/analysis-services.md)**<br /><br /> O[!INCLUDE[ssASnoversion_md](../includes/ssasnoversion-md.md)] é uma plataforma de dados analíticos e um conjunto de ferramentas para pessoal, equipe e business intelligence corporativo. Os servidores e designers de cliente dão suporte a soluções OLAP tradicionais, novas soluções de modelagem de tabela, bem como análises de autoatendimento e colaboração por meio do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)], o Excel e um ambiente do SharePoint Server. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] também inclui Mineração de Dados para que você possa descobrir os padrões e as relações ocultas dentro de grandes volumes de dados.|    
|![Reporting Services](../sql-server/media/reporting-services.png "Reporting Services")|**[Reporting Services](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)**<br /><br /> O Reporting Services oferece a funcionalidade de relatórios corporativos habilitados para a Web.  É possível criar relatórios que se conectam a conteúdos de várias fontes de dados, publicar relatórios em diversos formatos e centralizar o gerenciamento de segurança e de assinaturas.|
|![R Server](../sql-server/media/r-server.png "R Server")|**[Serviços de Machine Learning](../advanced-analytics/r-services/r-services.md)**<br /><br /> Os serviços do Microsoft Machine Learning dão suporte à integração de aprendizado de máquina em fluxos de trabalho da empresa usando as linguagens populares R e Python.<br /><br /> Os Serviços de Machine Learning (no banco de dados) integram R e Python com o SQL Server, facilitando a criação, a readaptação e a pontuação dos modelos ao chamar procedimentos armazenados.  O Microsoft Machine Learning Server dá suporte de nível corporativo para R e Python, sem a necessidade do SQL Server.|
|![Data Quality Services](../sql-server/media/data-quality-services.png "Data Quality Services")|**[Data Quality Services](../data-quality-services/data-quality-services.md)**<br /><br /> O SQL Server Data Quality Services (DQS) fornece uma solução de limpeza de dados controlada por conhecimento. O DQS permite que você crie uma base de dados de conhecimento e use-a para realizar a correção de dados e a eliminação de duplicação de seus dados, usando meios interativos e por computador. Você pode usar serviços de dados de referência baseados em nuvem e criar uma solução de gerenciamento de dados que integra o DQS com o SQL Server Integration Services e o Master Data Services.|
|![Serviços de replicação](../sql-server/media/replication-services.png "Serviços de replicação")|**[Replicação](../relational-databases/replication/sql-server-replication.md)**<br /><br /> A replicação é um conjunto de tecnologias para copiar e distribuir dados e objetos de um banco de dados para outro e, em seguida, sincronizar entre os bancos de dados para manter a consistência. Ao usar a replicação, é possível distribuir dados para diferentes locais e para usuários remotos e móveis através de redes locais e de longa distância, conexões discadas, conexões sem-fio e a Internet.|
|![Master Data Services](../sql-server/media/master-data-services.png)|**[Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md)**<br /><br /> [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] é a solução do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para gerenciamento de dados mestre. Uma solução criada no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ajuda a assegurar que o relatório e a análise sejam baseados nas informações corretas. Usando o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você cria um repositório central para seus dados mestres e mantém um registro auditável e seguro desses dados conforme eles forem alterados com o tempo.|

## <a name="migrate-and-move-data"></a>Migrar e mover dados
- [Importar e exportar dados com o Assistente de Importação e Exportação do SQL Server](../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)
- [Assistente de migração de dados da Microsoft](https://www.microsoft.com/download/details.aspx?id=53595)
- [Migrar seu banco de dados do SQL Server para o Banco de dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-migrate-your-sql-server-database)

## <a name="earlier-sql-server-versions"></a>Versões anteriores do SQL Server
- [Centro de atualização do SQL Server – links e informações para todas as versões com suporte](https://msdn.microsoft.com/library/ff803383.aspx)
- [Documentação do SQL Server 2014](https://msdn.microsoft.com/library/ms130214(v=sql.120).aspx)
- [Documentação do SQL Server 2012](https://technet.microsoft.com/library/bb418433(v=sql.10).aspx)  
- [Documentação do SQL Server 2008 R2](https://msdn.microsoft.com/library/hh278298(v=sql.10).aspx)  
- [Documentação do SQL Server 2008](https://msdn.microsoft.com/library/hh994727(v=sql.10).aspx) 
- [Documentação arquivada do SQL Server 2005](https://msdn.microsoft.com/library/hh278313(v=sql.10).aspx)    

## <a name="samples"></a>Exemplos  
- [Banco de dados de exemplo do Wide World Importers](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx)  
- [Bancos de dados e scripts de exemplo do AdventureWorks para SQL Server 2016](https://www.microsoft.com/download/details.aspx?id=49502) 
- [Exemplos de SQL Server no GitHub](https://github.com/Microsoft/sql-server-samples) 
   
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
