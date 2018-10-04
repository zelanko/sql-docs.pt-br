---
title: Remover referências a tabelas do sistema não documentadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- undocumented system tables [SQL Server]
- system tables [SQL Server]
ms.assetid: 010b1236-2219-4bf4-a6db-e3fc3abfa37a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c656f11c212b703f6a9a71a1392b5d0685b4c179
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48158276"
---
# <a name="remove-references-to-undocumented-system-tables"></a>Remover referências a tabelas do sistema não documentadas
  Muitas tabelas do sistema que não foram documentadas em versões anteriores foram alteradas ou deixaram de existir. Portanto, utilizar essas tabelas após a atualização pode causar erros. O Supervisor de Atualização procura referências a nomes de tabelas do sistema, portanto ele reportará referências a qualquer tabela do usuário que contenha o mesmo nome de uma tabela do sistema.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 As seguintes tabelas do sistema não documentadas foram removidas:  
  
-   **spt_datatype_info**  
  
-   **spt_datatype_info_ext**  
  
-   **spt_provider_types**  
  
-   **spt_server_info**  
  
-   **spt_values**  
  
-   **sysfulltextnotify**  
  
-   **syslocks**  
  
-   **sysproperties**  
  
-   **sysprotects_aux**  
  
-   **sysprotects_view**  
  
-   **SYSREMOTE_CATALOGS**  
  
-   **SYSREMOTE_COLUMN_PRIVILEGES**  
  
-   **SYSREMOTE_COLUMNS**  
  
-   **SYSREMOTE_FOREIGN_KEYS**  
  
-   **SYSREMOTE_INDEXES**  
  
-   **SYSREMOTE_PRIMARY_KEYS**  
  
-   **SYSREMOTE_PROVIDER_TYPES**  
  
-   **SYSREMOTE_SCHEMATA**  
  
-   **SYSREMOTE_STATISTICS**  
  
-   **SYSREMOTE_TABLE_PRIVILEGES**  
  
-   **SYSREMOTE_TABLES**  
  
-   **SYSREMOTE_VIEWS**  
  
-   **syssegments**  
  
-   **sysxlogins**  
  
## <a name="corrective-action"></a>Ação corretiva  
 Modifique seus aplicativos de acordo com a tabela a seguir:  
  
|Em vez de|Use|  
|----------------|---------|  
|**sysfulltextnotify**|Propriedade**TableFulltextPendingChanges** da função OBJECTPROPERTYEX.|  
|**syslocks**|Exibição de gerenciamento dinâmico**sys.dm_tran_locks** , sp_lock ou exibição de compatibilidade **sys.syslockinfo** .|  
|**sysproperties**|Exibição de catálogo**sys.extended_properties** ou função **fn_listextendedproperty** |  
|**sysxlogins**|Exibição de catálogo**sys.server_principals** ou exibição de compatibilidade **syslogins** .|  
|Todas as tabelas **spt_** .|Não há substituição disponível.|  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
