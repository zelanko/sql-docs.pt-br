---
title: Novidades no SQL Server 2016
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
keywords:
- novo sql server
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 39be659b50c7cc068c3887a0c0139b312c46cf0b
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58657980"
---
# <a name="whats-new-in-sql-server-2016"></a>Novidades no SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]  
 Com o SQL Server 2016, você pode compilar aplicativos críticos inteligentes usando uma plataforma de banco de dados híbrido escalonável que contém tudo integrado, desde desempenho na memória e a segurança avançada até análise no banco de dados. A versão do SQL Server 2016 adiciona novos recursos de segurança, recursos de consulta, integração do Hadoop com a nuvem, análise R e muito mais, juntamente com vários aprimoramentos e melhorias. 

Esta página fornece informações de resumo e links para informações mais detalhadas de novidades do SQL Server 2016 para cada componente do SQL Server. 

![SQL Server 2016](../sql-server/media/sql-server-2016.png)

 **Experimente o SQL Server hoje mesmo!** 
- Baixe **gratuitamente** a [**edição do desenvolvedor do SQL Server 2016!**](https://www.microsoft.com/cloud-platform/sql-server-editions-developers).
- Baixe a versão mais recente do [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md). 
- Tem uma conta do Azure? Ative uma [Máquina Virtual com o SQL Server 2016 já instalado](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftsqlserver.sql2016sp1-ws2016).

## <a name="sql-server-2016-database-engine"></a>Mecanismo de Banco de Dados do SQL Server 2016
- Agora você pode configurar **vários arquivos de banco de dados tempDB** durante a instalação e configuração do SQL Server.
- Novo **Repositório de Consultas** armazena textos de consulta, planos de execução e métricas de desempenho no banco de dados, permitindo monitoramento e solução de problemas de desempenho com facilidade. Um painel mostra quais consultas consumiram mais tempo, memória ou recursos de CPU.
- As **tabelas temporais** são tabelas de histórico que registram todas as alterações de dados, incluindo as datas e horas em que ocorreram.
- O novo **suporte interno a JSON** no SQL Server dá suporte a importações, exportações, análise e armazenamento de JSON.
- O novo mecanismo de consulta **PolyBase** integra o SQL Server com dados externos no Hadoop ou no Armazenamento de Blobs do Azure. Você pode importar e exportar dados, bem como executar consultas.
- O novo recurso **Stretch Database** permite que você arquive dados de forma dinâmica e segura a partir de um banco de dados SQL Server local para um banco de dados SQL do Azure na nuvem. O SQL Server consulta automaticamente os dados locais e remotos em bancos de dados vinculados. 
- **OLTP in-memory:** 
    - Agora dá suporte a restrições FOREIGN KEY, UNIQUE e CHECK e procedimentos armazenados compilados nativos OR, NOT, SELECT DISTINCT, OUTER JOIN e subconsultas em SELECT.
    - Dá suporte a tabelas de até 2 TB (acima de 256 GB). 
    - Tem aprimoramentos de índice de armazenamento de coluna para classificação e suporte ao Grupo de Disponibilidade AlwaysOn.
- Novos recursos de segurança:
    - **Always Encrypted:** Quando habilitado, somente o aplicativo que tem a chave de criptografia pode acessar os dados confidenciais criptografados no banco de dados SQL Server 2016. A chave nunca é passada para o SQL Server.
    - **Máscara de Dados Dinâmicos:** Se especificada na definição da tabela, os dados mascarados ficarão ocultos da maioria dos usuários e apenas os usuários com a permissão UNMASK poderão ver os dados concluídos.
    - **Segurança em Nível de Linha:** O acesso a dados pode ser restringido no nível do mecanismo de banco de dados, portanto, os usuários veem apenas o que é relevante para eles. 

Confira [Mecanismo de banco de dados](../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md).
## <a name="sql-server-2016-analysis-services-ssas"></a>SSAS (SQL Server 2016 Analysis Services)
O SQL Server 2016 Analysis Services fornece melhor desempenho, criação, gerenciamento de banco de dados, filtragem, processamento e muito mais para bancos de dados de modelo de tabela com base no **nível de compatibilidade 1200**.
- **[SQL Server R Services](../advanced-analytics/r-services/what-s-new-in-sql-server-r-services.md)** integram a linguagem de programação R, usada para análise estatística, ao SQL Server. 
- O novo **Verificador de Consistência de Banco de Dados (DBCC)** é executado internamente para detectar possíveis problemas de corrupção de dados.
- **Consulta Direta**, que consulta os dados externos ativos em vez de importá-los primeiro, agora dá suporte a mais fontes de dados, incluindo SQL Azure, Oracle e Teradata. 
- Há diversas **funções DAX (Expressões de Acesso a Dados) novas**.
- O novo namespace **[Microsoft.AnalysisServices.Tabular](https://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)** gerencia instâncias de modo de tabela e modelos. 
- Os [Objetos de Gerenciamento do Analysis Services (AMO)](https://msdn.microsoft.com/library/mt436122.aspx) foram refatorados para incluir um segundo assembly, **Microsoft.AnalysisServices.Core.dll**.

Confira [Mecanismo do Analysis Services (SSAS)](../analysis-services/what-s-new-in-analysis-services.md). 

## <a name="sql-server-2016-integration-services-ssis"></a>SSIS (SQL Server 2016 Integration Services)
- Suporte a **Grupos de Disponibilidade Always On**
- **Implantação de pacotes incremental**
- Suporte a **Always Encrypted**
- Nova função de nível de banco de dados **ssis_logreader**
- Novo **nível de registro em log personalizado**
- **Nomes de coluna para erros** no fluxo de dados 
- Novos **conectores**
- Suporte para o **HDFS (sistema de arquivos do Hadoop)**

Confira [Integration Services (SSIS)](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md).

## <a name="sql-server-2016-master-data-services-mds"></a>SQL Server 2016 Master Data Services (MDS)
- **Aprimoramentos de hierarquia derivados**, incluindo suporte para hierarquias de muitos para muitos e recursiva
- Filtragem de **atributo baseado em domínio**
- **Sincronização de entidade** para compartilhar dados de entidade entre modelos
- Fluxos de trabalho de aprovação por meio de **conjuntos de alterações**
- **Índices personalizados** para melhorar o desempenho da consulta
- Novos **níveis de permissão** para segurança aprimorada
- Experiência de **gerenciamento de regras de negócio** reformulada

Confira [MDS (Master Data Services)](../master-data-services/what-s-new-in-master-data-services-mds.md).

## <a name="sql-server-2016-reporting-services-ssrs"></a>SQL Server 2016 Reporting Services (SSRS)
A Microsoft renovou completamente o Reporting Services nesta versão. 
- Novo **Portal de Relatório da Web** com o recurso de KPI
- Novo **Publicador de Relatórios Móveis**
- **Mecanismo de renderização de relatório reprojetado** que dá suporte a HTML5 
- Novos **tipos de gráfico** mapa de árvore e explosão solar 

Confira [Reporting Services (SSRS)](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md).

## <a name="next-steps"></a>Próximas etapas   
- [Instalação do SQL Server](../database-engine/install-windows/installation-for-sql-server-2016.md)   
- [Notas de Versão do SQL Server 2016.](../sql-server/sql-server-2016-release-notes.md) 
- [Folha de dados do SQL Server 2016](https://download.microsoft.com/download/C/5/3/C53C3AEF-653C-4598-8721-D522E8AC6A3A/SQL_Server_2016_Everything_Built-In_Datasheet_EN_US.pdf)
- [Recursos com suporte nas edições do SQL Server](https://msdn.microsoft.com/library/cc645993.aspx)
- [Requisitos de hardware e software para a instalação do SQL Server 2016](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
- [Instalar o SQL Server 2016 por meio do Assistente de Instalação](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
- [Configuração e instalação de manutenção](https://msdn.microsoft.com/library/6df72a78-6b36-4bc1-948e-04b4ebe46094)
- [Novo módulo do PowerShell no SQL](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update/)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
