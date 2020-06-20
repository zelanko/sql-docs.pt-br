---
title: Modificar aplicativos para esperar valores bigint de sysperfinfo. cntr_value | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- sysperfinfo
- bigint values [SQL Server]
ms.assetid: b0345303-6e9a-4078-8148-6e1bce207b8c
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 108a9b981debc95e182b16847c39a03d4b242088
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012205"
---
# <a name="modify-applications-to-expect-bigint-values-from-sysperfinfocntr_value"></a>Modificar aplicativos para esperar valores bigint de sysperfinfo.cntr_value
  sysperfinfo retorna um `bigint` valor para a coluna cntr_value.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Modifique os aplicativos que usam sysperfinfo para assegurar que eles possam lidar com os valores `bigint` da coluna cntr_value.  
  
> [!NOTE]  
>  sysperfinfo é uma exibição de compatibilidade. Em vez disso, você deve usar o gerenciamento dinâmico sys.dm_os_performance_counter.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
