---
title: Executar o Windows PowerShell no SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c6d71f1158ef73b84e5b04dcc9a1970bfd7dce35
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72783102"
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>Executar o Windows PowerShell no SQL Server Management Studio
  Você pode iniciar sessões do Windows PowerShell no **Pesquisador de Objetos** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]inicia o Windows PowerShell, carrega `sqlps` o módulo e define o contexto do caminho para o nó associado na árvore do pesquisador de **objetos** .  
  
## <a name="before-you-begin"></a>Antes de começar  
 Quando você especificar a execução do PowerShell para um objeto no **Pesquisador de Objetos**, o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] iniciará uma sessão do Windows PowerShell na qual os snap-ins do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell foram carregados e registrados. O caminho da sessão é predefinido no local do objeto em que você clicou com o botão direito no Pesquisador de Objetos. Por exemplo, se você clicar com o botão direito do mouse no objeto de banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] no Pesquisador de Objetos e selecionar **Iniciar PowerShell**, o caminho do Windows PowerShell será definido da seguinte forma:  
  
```
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## <a name="to-run-powershell-from-sql-server-management-studio"></a>Para executar o PowerShell no SQL Server Management Studio 
  
1.  Abra o **Pesquisador de Objetos**.  
  
2.  Navegue até o nó do objeto que será utilizado.  
  
3.  Clique com o botão direito do mouse no objeto e selecione **Iniciar PowerShell**.  
  
## <a name="permissions"></a>Permissões  
 Quando aberto no [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], o PowerShell não é executado com privilégios de Administrador que podem impedir algumas atividades como chamadas ao WMI.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server PowerShell](sql-server-powershell.md)  
