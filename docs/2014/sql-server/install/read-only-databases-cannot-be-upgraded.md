---
title: Bancos de dados somente leitura não podem ser atualizados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- database cannot be upgraded
ms.assetid: 27964211-ea30-4390-b791-dcf225fb9ae7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 414b26cf860ab32bb11beaa1ccbef3316c68f557
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093367"
---
# <a name="read-only-databases-cannot-be-upgraded"></a>Bancos de dados somente leitura não podem ser atualizados
  O Supervisor de Atualização determinou que alguns bancos de dados nesta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não podem ser atualizados.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrição  
 Um banco de dados somente leitura foi detectado. Para atualizar o banco de dados, a Instalação deve poder gravar no banco de dados.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Quando ninguém está usando o banco de dados, use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Manager [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ou a instrução ALTER DATABASE para alterar o banco de dados para leitura e gravação. As instruções a seguir alteram o banco de dados para leitura e gravação:  
  
```  
USE master;  
GO  
ALTER DATABASE <database name>  
SET READ_WRITE;  
GO  
```  
  
 Para obter mais informações sobre a instrução ALTER DATABASE, consulte o tópico ‘ALTER DATABASE ([!INCLUDE[tsql](../../includes/tsql-md.md)])’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
