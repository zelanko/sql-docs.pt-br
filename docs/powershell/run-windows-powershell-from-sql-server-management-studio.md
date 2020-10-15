---
title: Executar o Windows PowerShell no SQL Server Management Studio | Microsoft Docs
description: Saiba como iniciar uma sessão do Windows PowerShell no Pesquisador de Objetos no SQL Server Management Studio, com o caminho predefinido com a localização de objetos de sua escolha.
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: ''
ms.date: 03/14/2017
ms.openlocfilehash: c074b0f0ed5f5b041a8a4c4ed341837fec2b1926
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "92006163"
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>Executar o Windows PowerShell no SQL Server Management Studio

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Você pode iniciar sessões do Windows PowerShell no **Pesquisador de Objetos** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] inicia o Windows PowerShell, carrega o módulo do **SqlServer** e define o contexto de caminho ao nó associado na árvore do **Pesquisador de Objetos**.  

[!INCLUDE [sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

Quando você especificar a execução do PowerShell para um objeto no **Pesquisador de Objetos**, o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] iniciará uma sessão do Windows PowerShell na qual os snap-ins do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell foram carregados e registrados. O caminho da sessão é predefinido no local do objeto no qual você clicou com o botão direito no Pesquisador de Objetos. Por exemplo, se você clicar com o botão direito do mouse no objeto de banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] no Pesquisador de Objetos e selecionar **Iniciar PowerShell**, o caminho do Windows PowerShell será definido da seguinte forma:  

```powershell
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```

## <a name="run-powershell"></a>Executar o PowerShell

### <a name="to-run-powershell-from-sql-server-management-studio"></a>Para executar o PowerShell no SQL Server Management Studio

1. Abra o **Pesquisador de Objetos**.

2. Navegue até o nó do objeto que será utilizado.

3. Clique com o botão direito do mouse no objeto e selecione **Iniciar PowerShell**.

## <a name="permissions"></a>Permissões

Quando aberto no [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], o PowerShell não é executado com privilégios de Administrador, que podem impedir algumas atividades como chamadas ao WMI.  
  
## <a name="see-also"></a>Consulte Também

- [SQL Server PowerShell](sql-server-powershell.md)