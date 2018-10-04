---
title: SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d8a161aeef437e04a3d6e7300a79af5fa0671568
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48068736"
---
# <a name="sql-server-powershell"></a>SQL Server PowerShell
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] oferece suporte ao Windows PowerShell, que é um shell de geração de script avançado que permite aos administradores e desenvolvedores automatizarem a administração de servidor e a implantação de aplicativo. A linguagem do Windows PowerShell suporta uma lógica mais complexa que os scripts [!INCLUDE[tsql](../includes/tsql-md.md)] , fornecendo aos administradores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a capacidade de criar scripts de administração avançados. Os scripts do Windows PowerShell também podem ser usados para administrar outros produtos de servidor do [!INCLUDE[msCoName](../includes/msconame-md.md)] . Isso fornece aos administradores uma linguagem de criação de scripts comum aos servidores.  
  
## <a name="sql-server-powershell-components"></a>Componentes do SQL Server PowerShell  
 O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornece um módulo de Windows PowerShell nomeado `sqlps` que é usado para importar os componentes [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um ambiente de Windows PowerShell 2.0 ou script. O módulo `sqlps` carrega dois snap-ins do Windows PowerShell que implementam:  
  
-   Um provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , que ativa um mecanismo de navegação simples semelhante aos caminhos de sistema de arquivos. É possível criar caminhos semelhantes aos caminhos de sistema de arquivos, onde a unidade é associada ao modelo de objeto de gerenciamento do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e os nós baseiam-se nas classes de modelo do objeto. Você pode usar os comandos conhecidos, como **cd** e **dir** , para navegar pelos caminhos de maneira semelhante à forma como navega pelas pastas em uma janela do prompt de comando. Também pode usar outros comandos, como **ren** ou **del**, para executar ações nos nós no caminho.  
  
-   Um conjunto de cmdlets, que são comandos usados em scripts do Windows PowerShell para especificar uma ação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . O módulo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] oferecem suporte a ações, como, por exemplo, a execução de um script **sqlcmd** que contém instruções [!INCLUDE[tsql](../includes/tsql-md.md)] ou XQuery.  
  
 Para saber mais sobre o Windows PowerShell, consulte o [Guia de Introdução do Windows PowerShell](http://msdn.microsoft.com/library/hh857337.aspx).  
  
## <a name="sql-server-versions"></a>Versões do SQL Server  
 Os componentes do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] PowerShell podem ser usados para gerenciar instâncias do [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)] ou posterior. Instâncias do [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] devem estar executando o SP2 ou posterior. Instâncias do [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)] devem estar executando o SP4 ou posterior. Quando os componentes do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] PowerShell são usados com versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], eles ficam limitados à funcionalidade disponível nessas versões.  
  
## <a name="sql-server-powershell-tasks"></a>Tarefas do SQL Server PowerShell  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve o mecanismo preferencial para executar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] componentes do PowerShell; para abrir uma sessão do PowerShell e carregar o `sqlps` módulo. O módulo `sqlps` carrega o provedor e os cmdlets do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell, e os assemblies SMO (SQL Server Management Object) usados pelo provedor e cmdlets.|[Importar o módulo SQLPS](../database-engine/import-the-sqlps-module.md)|  
|Descreve como carregar apenas os assemblies SMO sem o provedor ou cmdlets.|[Carregar os assemblies SMO no Windows PowerShell](load-the-smo-assemblies-in-windows-powershell.md)|  
|Descreve como executar uma sessão do Windows PowerShell clicando com o botão direito do mouse em um nó no **Pesquisador de Objeto**. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] inicia uma sessão do Windows PowerShell, carrega o `sqlps` módulo e define o caminho do provedor do SQL Server para o objeto selecionado.|[Executar o Windows PowerShell no SQL Server Management Studio](run-windows-powershell-from-sql-server-management-studio.md)|  
|Descreve como criar as etapas de trabalho do SQL Server Agent que executam um script do Windows PowerShell. Os trabalhos podem ser agendados para execução em horários específicos ou em resposta a eventos.|[Executar etapas do Windows PowerShell no SQL Server Agent] (run-windows-powershell-steps-in-sql-server-agent.md
)|  
|Descreve como usar o provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para navegar por uma hierarquia de objetos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|[Provedor do SQL Server PowerShell](sql-server-powershell-provider.md)|  
|Descreve como usar o cmdlets [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que especifica ações [!INCLUDE[ssDE](../includes/ssde-md.md)] como executar um script [!INCLUDE[tsql](../includes/tsql-md.md)] .|[Usar cmdlets do Mecanismo de Banco de Dados](../database-engine/use-the-database-engine-cmdlets.md)|  
|Descreve como especificar identificadores delimitados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que contêm caracteres sem suporte do Windows PowerShell.|[Identificadores do SQL Server no PowerShell](sql-server-identifiers-in-powershell.md)|  
|Descreve como fazer conexões para Autenticação do SQL Server. Por padrão, os componentes do SQL Server PowerShell usam conexões de Autenticação do Windows que usam as credenciais do Windows do processo que executa o Windows PowerShell.|[Gerenciar a autenticação no Mecanismo de Banco de Dados com o PowerShell](manage-authentication-in-database-engine-powershell.md)|  
|Descreve como usar variáveis implementadas pelo provedor do SQL Server PowerShell para controlar quantos objetos são listados ao usar a conclusão de guia do Windows PowerShell. Isso é particularmente útil ao trabalhar em bancos de dados que contêm um grande número de objetos.|[Gerenciar preenchimento com Tab &#40;SQL Server PowerShell&#41;](manage-tab-completion-sql-server-powershell.md)|  
|Descreve como usar o Get-Help para obter informações sobre componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no ambiente Windows PowerShell.|[Get Help SQL Server PowerShell](../database-engine/get-help-sql-server-powershell.md)|  
  
  
