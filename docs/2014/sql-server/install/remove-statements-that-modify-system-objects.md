---
title: Remover instruções que modificam objetos do sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- direct system catalog updates [SQL Server]
- system catalogs [SQL Server]
ms.assetid: 221b46c2-c27e-4df8-bd8c-8b990d6d5e98
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0f65d379076eb213971bba97b970b8aa866ca3a5
ms.sourcegitcommit: 5905c29b5531cef407b119ebf5a120316ad7b713
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66428879"
---
# <a name="remove-statements-that-modify-system-objects"></a>Remover instruções que modificam objetos do sistema
  O Supervisor de Atualização detectou instruções que atualizam o catálogo do sistema. Atualizações diretas no catálogo do sistema não são permitidas. Modifique seus scripts SQL para usar APIs oficiais e documentadas.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrição  
 Atualizações diretas no catálogo do sistema não são permitidas. Qualquer tentativa para fazer essas atualizações gerará o erro seguinte:  
  
 `Server: Msg 259, Level 16, State 1, Line 1`  
  
 `Ad hoc updates to system catalogs are not allowed.`  
  
## <a name="corrective-action"></a>Ação corretiva  
 Modifique seus scripts SQL para usar APIs oficiais e documentadas. Por exemplo, use ALTER DATABASE *database_name* SET EMERGENCY em vez de executar uma instrução UPDATE na tabela de sistema **sysdatabases** .  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](https://docs.microsoft.com/sql/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
