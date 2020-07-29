---
title: Visão geral das ferramentas do SQL
description: Ferramentas de gerenciamento e consulta do SQL para SQL Server, SQL do Azure (Banco de Dados SQL do Azure, instância gerenciada do SQL do Azure, máquinas virtuais do SQL) e SQL Data Warehouse do Azure.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ''
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 02/04/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 59a376b17c6e4b396dba24999a52bf37ecc27988
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009603"
---
# <a name="sql-tools-overview"></a>Visão geral das ferramentas do SQL

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Para gerenciar seu banco de dados, você precisa de uma ferramenta. Quer seus bancos de dados sejam executados na nuvem, no Windows, no macOS ou no [Linux](../linux/sql-server-linux-overview.md), sua ferramenta não precisa ser executada na mesma plataforma que o banco de dados.

Você pode ver os links para as diferentes ferramentas do SQL nas tabelas a seguir.

> [!Note]
> Para baixar o SQL Server, confira [Instalar o SQL Server](../database-engine/install-windows/install-sql-server.md).

## <a name="recommended-tools"></a>Ferramentas recomendadas

As ferramentas a seguir fornecem uma GUI (interface gráfica do usuário).

| Ferramenta | DESCRIÇÃO | Sistema operacional |
|:--|:--|:--|
| [ **![Imagem do ADS](../tools/media/overview-sql-tools/azure-data-studio.svg)</br></br>Azure Data Studio**](../azure-data-studio/download.md) | Um editor leve que pode executar consultas SQL sob demanda, exibir e salvar resultados como texto, JSON ou Excel. Edite dados, organize suas conexões de banco de dados favoritas e procure objetos de banco de dados em uma experiência de navegação de objetos familiar. | **Windows</br>macOS</br>Linux** |
| [ **![Imagem do SSMS](../tools/media/overview-sql-tools/ssms.svg)</br></br>SSMS (SQL Server Management Studio)** ](../ssms/download-sql-server-management-studio-ssms.md) | Gerencie uma instância do SQL Server ou um banco de dados com compatibilidade total com a GUI. Acesse, configure, gerencie, administre e desenvolva todos os componentes do SQL Server, do Banco de Dados SQL do Azure e do SQL Data Warehouse. Fornece um utilitário abrangente que combina um amplo grupo de ferramentas gráficas com vários editores de script avançados para fornecer acesso ao SQL para desenvolvedores e administradores de banco de dados de todos os níveis de conhecimento. | **Windows** |
| [ **![Imagem do SSDT](../tools/media/overview-sql-tools/ssdt.svg)</br>SSDT (SQL Server Data Tools)** ](../ssdt/download-sql-server-data-tools-ssdt.md) | Uma moderna ferramenta de desenvolvimento para criar bancos de dados relacionais do SQL Server, bancos de dados SQL do Azure, modelos de dados do AS (Analysis Services), pacotes do IS (Integration Services) e relatórios do RS (Reporting Services). Com o SSDT, você pode projetar e implantar qualquer tipo de conteúdo do SQL Server com a mesma facilidade com que desenvolve um aplicativo no **[Visual Studio](https://visualstudio.microsoft.com/downloads/)** . | **Windows** |
| [ **![Imagem do VS Code](../tools/media/overview-sql-tools/visual-studio-code.svg)</br></br>Visual Studio Code**](https://code.visualstudio.com/) | A **[extensão mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)** para Visual Studio Code é a extensão do SQL Server oficial que é compatível com conexões com SQL Server e com a experiência de edição avançada para o T-SQL no Visual Studio Code. Escreva scripts T-SQL em um editor leve. | **Windows</br>macOS</br>Linux** |

## <a name="command-line-tools"></a>Ferramentas da linha de comando

As ferramentas a seguir são as principais ferramentas de linha de comando.

| Ferramenta | DESCRIÇÃO | Sistema operacional |
|:--|:--|:--|
|[**bcp**](bcp-utility.md)|O utilitário **bcp** (**b**ulk **c**opy **p**rogram) copia dados em massa entre uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e um arquivo de dados em um formato especificado pelo usuário.| **Windows</br>macOS</br>Linux** |
|[**mssql-cli (versão prévia)** ](mssql-cli.md)|O **mssql-cli** é uma ferramenta de linha de comando interativa para consultar o SQL Server. Além disso, consulte o SQL Server com uma ferramenta de linha de comando com IntelliSense, realce de sintaxe e muito mais. | **Windows</br>macOS</br>Linux** |
|[**mssql-conf**](../linux/sql-server-linux-configure-mssql-conf.md) | O **mssql-conf** configura o SQL Server sendo executado no Linux. | **Linux** |
|[**mssql-scripter (versão prévia)** ](https://github.com/Microsoft/mssql-scripter) | O **mssql-scripter** é uma experiência de linha de comando de várias plataformas para criar scripts de bancos de dados SQL Server. | **Windows</br>macOS</br>Linux** |
| [**sqlcmd**](sqlcmd-utility.md) |O utilitário **sqlcmd** permite que você insira instruções de Transact-SQL, procedimentos do sistema e arquivos de script no prompt de comando. | **Windows</br>macOS</br>Linux** |
| [**sqlpackage**](sqlpackage.md) |O **sqlpackage** é um utilitário de linha de comando que automatiza diversas tarefas de desenvolvimento de banco de dados. |**Windows</br>macOS</br>Linux** |
|[**SQL Server PowerShell**](../powershell/sql-server-powershell.md)| O **SQL Server PowerShell** fornece cmdlets para trabalhar com o SQL. | **Windows</br>macOS</br>Linux** |

## <a name="migration-and-other-tools"></a>Migração e outras ferramentas

Estas ferramentas são usadas para migrar, configurar e fornecer outros recursos para bancos de dados SQL.

| Ferramenta | DESCRIÇÃO |
|:--|:--|
| **[Gerenciador de Configurações](../tools/configuration-manager/sql-server-configuration-manager-help.md)** | Use o SQL Server Configuration Manager para configurar os serviços do SQL Server e configurar a conectividade de rede. O Configuration Manager é executado no Windows|
| **[Assistente para Experimentos de Banco de Dados](../dea/database-experimentation-assistant-overview.md)** | Use o Assistente para Experimentos de Banco de Dados para avaliar uma versão de destino do SQL para uma determinada carga de trabalho. |
| **[Assistente de Migração de Dados](../dma/dma-overview.md)** | A ferramenta Assistente de Migração de Dados ajuda você a atualizar para uma plataforma de dados moderna, detectando problemas de compatibilidade que podem afetar a funcionalidade do banco de dados em sua nova versão do SQL Server ou do Banco de Dados SQL do Azure. |
| **[Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md)** | Use o recurso Distributed Replay para ajudar a avaliar o impacto de futuras atualizações do SQL Server. Também use o Distributed Replay para ajudar a avaliar o impacto de atualizações de hardware e do sistema operacional e ajustes do SQL Server. |
| **[ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)** | O utilitário ssbdiagnose relata problemas em conversas do Service Broker ou na configuração de serviços do Service Broker. |
| **[Assistente de Migração do SQL Server](../ssma/sql-server-migration-assistant.md)** | Use o Assistente de Migração do SQL Server para automatizar a migração do banco de dados do Microsoft Access, do DB2, do MySQL, do Oracle e do Sybase para o SQL Server.|

Se você estiver procurando ferramentas adicionais não mencionadas nesta página, confira [Utilitários de prompt de comando SQL](command-prompt-utility-reference-database-engine.md) e [Baixar recursos e ferramentas estendidos do SQL Server](download-sql-feature-packs.md)