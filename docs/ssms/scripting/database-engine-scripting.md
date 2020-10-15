---
title: Geração de scripts do mecanismo de banco de dados
description: Saiba como você pode usar o ambiente de script do Microsoft PowerShell para gerenciar instâncias do Mecanismo de Banco de Dados do SQL Server e como você pode compilar e executar consultas do Mecanismo de Banco de Dados que contêm Transact-SQL e XQuery.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- scripts [SQL Server], PowerShell
- scripts [SQL Server]
- scripting [SQL Server Database Engine]
- scripting [SQL Server Database Engine], PowerShell
ms.assetid: 9978a884-59a2-4e7f-a82a-335149f3a261
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ae4d356751aa466b6ca13455c514cea91cd95c21
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92039070"
---
# <a name="database-engine-scripting"></a>Geração de scripts do mecanismo de banco de dados
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] oferece suporte ao ambiente de script do [!INCLUDE[msCoName](../../includes/msconame-md.md)] PowerShell para gerenciar instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e os objetos nas instâncias. Também é possível criar e executar consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que contêm [!INCLUDE[tsql](../../includes/tsql-md.md)] e XQuery em ambientes muito semelhantes aos ambientes de script.  
  
## <a name="sql-server-powershell"></a>SQL Server PowerShell  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui dois snap-ins do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell que implementam:  
  
-   Um provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell que expõe as hierarquias de modelos de objeto de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como caminhos do PowerShell que são semelhantes aos caminhos do sistema de arquivos. É possível usar as classes de modelo de objeto de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para gerenciar os objetos representados em cada nó do caminho.  
  
-   Um conjunto de cmdlets do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que implementa comandos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Um dos cmdlets é **Invoke-Sqlcmd**. Ele é usado para executar scripts de consulta do [!INCLUDE[ssDE](../../includes/ssde-md.md)] a serem executados com o utilitário **sqlcmd** .  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece estes recursos para execução do PowerShell:  
  
-   O módulo **sqlps** do PowerShell que pode ser importado para uma sessão do PowerShell; em seguida, o módulo carrega os snap-ins do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . É possível executar interativamente comandos do PowerShell ad hoc. É possível executar arquivos de script usando um comando como .\MyFolder\MyScript.ps1.  
  
-   Os arquivos de script do PowerShell podem ser usados como entrada para etapas de trabalho do PowerShell do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que executam os scripts em intervalos agendados ou em resposta a eventos do sistema.  
  
-   O utilitário **sqlps** que inicia o PowerShell e importa o módulo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Em seguida, você pode executar todas as ações com suporte no módulo. É possível iniciar o utilitário **sqlps** em um prompt de comando ou clicando com o botão direito do mouse nos nós da árvore do Pesquisador de Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio e selecionando **Iniciar PowerShell**.  
  
## <a name="database-engine-queries"></a>Consultas do mecanismo de banco de dados  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] contêm três tipos de elementos:  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
-   Instruções de linguagem XQuery  
  
-   Comandos e variáveis do utilitário **sqlcmd** .  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece três ambientes para criar e executar consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] :  
  
-   É possível executar e depurar consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] interativamente no Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. É possível codificar e depurar várias instruções em uma sessão e, em seguida, salvar todas as instruções em um único arquivo de script.  
  
-   O utilitário de prompt de comando do **sqlcmd** permite executar interativamente consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e também arquivos de script de consulta do [!INCLUDE[ssDE](../../includes/ssde-md.md)] existentes.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] normalmente são codificados interativamente no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usando o Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . O arquivo pode ser aberto posteriormente em um destes ambientes:  
  
-   Use o menu [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Abrir**/**do** para abrir o arquivo em uma nova janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Use o parâmetro **-i**_input_file_ para executar o arquivo com o utilitário **sqlcmd** .  
  
-   Use o parâmetro **-QueryFromFile** para executar o arquivo com o cmdlet **Invoke-Sqlcmd** em scripts do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell.  
  
-   Use etapas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent [!INCLUDE[tsql](../../includes/tsql-md.md)] para executar os scripts em intervalos agendados ou em resposta a eventos do sistema.  
  
 Além disso, você pode usar o Assistente para Gerar Scripts do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para gerar scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] . Você pode clicar com o botão direito do mouse no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e selecionar o item de menu **Gerar Script** . A opção**Gerar Script** inicia o assistente que fornece instruções para o processo de criação de um script.  
  
## <a name="database-engine-scripting-tasks"></a>Tarefas de scripts do mecanismo de banco de dados  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como usar código e editores de texto no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para desenvolver, depurar e executar interativamente scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] .|[Editores de consultas e de texto &#40;SQL Server Management Studio&#41;](../f1-help/database-engine-query-editor-sql-server-management-studio.md?view=sql-server-ver15)|  
|Descreve como usar o utilitário **sqlcmd** para executar scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] do prompt de comando, incluindo a capacidade de desenvolver scripts de maneira interativa.|[Tópicos de informações práticas sobre sqlcmd](./sqlcmd-start-the-utility.md)|  
|Descreve como integrar os componentes do SQL Server em um ambiente do Windows PowerShell e, então, compilar scripts do PowerShell para gerenciar instâncias e objetos do SQL Server.|[SQL Server PowerShell](../../powershell/sql-server-powershell.md)|  
|Descreve como usar o assistente para **Gerar e Publicar Scripts** para criar scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] que recriam um ou mais dos objetos de um banco de dados.|[Gerar scripts &#40;SQL Server Management Studio&#41;](./generate-scripts-sql-server-management-studio.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Utilitário sqlcmd](../../tools/sqlcmd-utility.md)   
 [Tutorial: Gravando instruções Transact-SQL](../../t-sql/tutorial-writing-transact-sql-statements.md)  
  
