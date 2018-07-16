---
title: Remover instruções que modificam objetos do sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- direct system catalog updates [SQL Server]
- system catalogs [SQL Server]
ms.assetid: 221b46c2-c27e-4df8-bd8c-8b990d6d5e98
caps.latest.revision: 21
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aca644a822673e4d373048fc0d3a95eb0cd6fdf6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37297808"
---
# <a name="remove-statements-that-modify-system-objects"></a>Remover instruções que modificam objetos do sistema
  O Supervisor de Atualização detectou instruções que atualizam o catálogo do sistema. Atualizações diretas no catálogo do sistema não são permitidas. Modifique seus scripts SQL para usar APIs oficiais e documentadas.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 Atualizações diretas no catálogo do sistema não são permitidas. Qualquer tentativa para fazer essas atualizações gerará o erro seguinte:  
  
 `Server: Msg 259, Level 16, State 1, Line 1`  
  
 `Ad hoc updates to system catalogs are not allowed.`  
  
## <a name="corrective-action"></a>Ação corretiva  
 Modifique seus scripts SQL para usar APIs oficiais e documentadas. Por exemplo, use ALTER DATABASE *database_name* SET EMERGENCY em vez de executar uma instrução UPDATE na tabela de sistema **sysdatabases** .  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
