---
title: Remover instruções que descartam objetos do sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- drop system objects [SQL Server]
ms.assetid: cdfc3c50-c801-4039-a4bf-b35f876f1c61
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4c017e6fedbc7fd994e5b2d2ca4de184a082da65
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007641"
---
# <a name="remove-statements-that-drop-system-objects"></a>Remover instruções que descartam objetos do sistema
  O Supervisor de Atualização detectou instruções que descartam objetos do sistema. Os objetos do sistema, incluindo procedimentos armazenados estendidos, são implantados no banco de dados de **recurso** (mssqlsystemresource) somente leitura e não podem ser descartados. Modifique seus aplicativos para revocar ou negar a permissão EXECUTE em objetos do sistema.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 Instruções como DROP TABLE, DROP PROCEDURE e **sp_dropextendedproc** não podem ser usadas para remover objetos do sistema, pois esses objetos são implantados no banco de dados de **recurso** somente leitura.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Remova todas as instruções que tentam descartar objetos do sistema de seus aplicativos. Modifique seus aplicativos para revocar ou negar a permissão EXECUTE em objetos do sistema. Como alternativa, você pode usar a ferramenta SAC (Configuração da Área de Superfície) para desabilitar alguns desses objetos. Por exemplo, o procedimento armazenado estendido **xp_cmdshell** pode ser desabilitado ou habilitado usando a ferramenta SAC.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
