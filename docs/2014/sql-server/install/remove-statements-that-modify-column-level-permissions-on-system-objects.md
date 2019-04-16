---
title: Remover instruções que modificam permissões em nível de coluna em objetos do sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- column-level permissions [SQL Server]
- removed statement permissions [SQL Server]
ms.assetid: 7f4fbbef-2696-4911-903b-63f6d9e4484a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f61990ae0eb35a399a1efca4a5a2cf754892e3d0
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582839"
---
# <a name="remove-statements-that-modify-column-level-permissions-on-system-objects"></a>Remover instruções que modificam permissões em nível de coluna nos objetos do sistema
  O Supervisor de Atualização detectou permissões em nível de coluna não padrão nos objetos do sistema. Essas alterações de permissão não serão mantidas quando você fizer a atualização. Além disso, não há mais suporte para permissões em nível de coluna nos objetos do sistema em versões posteriores. Remova as instruções que definem permissões em nível de coluna nos objetos do sistema dos seus aplicativos.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Remova as instruções do seu aplicativo que concedem, negam ou revocam permissões em nível de coluna dos objetos do sistema.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
