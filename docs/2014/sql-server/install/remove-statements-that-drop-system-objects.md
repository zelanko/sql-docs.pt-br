---
title: Remover instruções que descartam objetos do sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- drop system objects [SQL Server]
ms.assetid: cdfc3c50-c801-4039-a4bf-b35f876f1c61
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1d420e2dba1dfdb284b0002eca6d8408c4e019e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093082"
---
# <a name="remove-statements-that-drop-system-objects"></a>Remover instruções que descartam objetos do sistema
  O Supervisor de Atualização detectou instruções que descartam objetos do sistema. Os objetos do sistema, incluindo procedimentos armazenados estendidos, são implantados no banco de dados de **recurso** (mssqlsystemresource) somente leitura e não podem ser descartados. Modifique seus aplicativos para revocar ou negar a permissão EXECUTE em objetos do sistema.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrição  
 Instruções como DROP TABLE, DROP PROCEDURE e **sp_dropextendedproc** não podem ser usadas para remover objetos do sistema, pois esses objetos são implantados no banco de dados de **recurso** somente leitura.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Remova todas as instruções que tentam descartar objetos do sistema de seus aplicativos. Modifique seus aplicativos para revocar ou negar a permissão EXECUTE em objetos do sistema. Como alternativa, você pode usar a ferramenta SAC (Configuração da Área de Superfície) para desabilitar alguns desses objetos. Por exemplo, o procedimento armazenado estendido **xp_cmdshell** pode ser desabilitado ou habilitado usando a ferramenta SAC.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
