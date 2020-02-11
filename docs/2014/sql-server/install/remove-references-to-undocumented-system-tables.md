---
title: Remover referências a tabelas do sistema não documentadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- undocumented system tables [SQL Server]
- system tables [SQL Server]
ms.assetid: 010b1236-2219-4bf4-a6db-e3fc3abfa37a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 06249aa1849a1be9af40e183724e85b0f318f3dc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093153"
---
# <a name="remove-references-to-undocumented-system-tables"></a>Remover referências a tabelas do sistema não documentadas
  Muitas tabelas do sistema que não foram documentadas em versões anteriores foram alteradas ou deixaram de existir. Portanto, utilizar essas tabelas após a atualização pode causar erros. O Supervisor de Atualização procura referências a nomes de tabelas do sistema, portanto ele reportará referências a qualquer tabela do usuário que contenha o mesmo nome de uma tabela do sistema.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>DESCRIÇÃO  
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
  
|Em vez de|Uso|  
|----------------|---------|  
|**sysfulltextnotify**|Propriedade **TableFulltextPendingChanges** da função OBJECTPROPERTYEX.|  
|**syslocks**|**Sys. dm_tran_locks** exibição de gerenciamento dinâmico, ou sp_lock, ou a exibição de compatibilidade **Sys. syslockinfo** .|  
|**sysproperties**|a exibição de catálogo **Sys. extended_properties** ou a função **fn_listextendedproperty**|  
|**sysxlogins**|exibição de catálogo **Sys. server_principals** ou exibição de compatibilidade **syslogins** .|  
|Todas as tabelas **spt_** .|Não há substituição disponível.|  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
