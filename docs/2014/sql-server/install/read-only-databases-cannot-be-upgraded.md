---
title: Bancos de dados somente leitura não podem ser atualizados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- database cannot be upgraded
ms.assetid: 27964211-ea30-4390-b791-dcf225fb9ae7
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 11f94ceed205d8984ed5a253e1d989211012f10f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130507"
---
# <a name="read-only-databases-cannot-be-upgraded"></a>Bancos de dados somente leitura não podem ser atualizados
  O Supervisor de Atualização determinou que alguns bancos de dados nesta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não podem ser atualizados.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 Um banco de dados somente leitura foi detectado. Para atualizar o banco de dados, a Instalação deve poder gravar no banco de dados.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Quando não estiver usando o banco de dados, use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Manager [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ou a instrução ALTER DATABASE para alterar o banco de dados para leitura e gravação. As instruções a seguir alteram o banco de dados para leitura e gravação:  
  
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
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
