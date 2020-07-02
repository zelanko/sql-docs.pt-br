---
title: sys. dm_tran_commit_table (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_commit_table
- dm_tran_commit_table_TSQL
- sys.dm_tran_commit_table
- sys.dm_tran_commit_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_commit_table dynamic management view
ms.assetid: 732d23c5-1f6c-4e96-bc85-8f29b520cf0e
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 863da6499e788b07576066a1890c4532f3a06456
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720374"
---
# <a name="change-tracking---sysdm_tran_commit_table"></a>Controle de Alterações-sys. dm_tran_commit_table
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Exibe uma linha para cada transação confirmada para uma tabela controlada pelo controle de alterações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A exibição de gerenciamento de sys.dm_tran_commit_table, que é fornecida para fins de suporte e expõe as informações relacionadas a transações que o controle de alterações armazena na tabela do sistema sys.syscommittab. A tabela sys.syscommittab fornece um mapeamento persistente eficiente de uma ID de transação específica ao banco de dados para o LSN (número de sequência de log) de confirmação da transação e para o carimbo de data/hora da confirmação. Os dados armazenados na tabela sys.syscommittab e expostos nessa exibição de gerenciamento estão sujeitos à limpeza de acordo com o período de retenção especificado quando o controle de alterações foi configurado.  
  
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys. dm_pdw_nodes_tran_commit_table**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|commit_ts|**bigint**|Um número que aumenta de forma monotônica que serve como um carimbo de data/hora específico a um banco de dados para cada transação confirmada.|  
|xdes_id|**bigint**|Uma ID interna específica do banco de dados para a transação.|  
|commit_lbn|**bigint**|O número do bloco de logs que contém o registro de log de confirmação para a transação.|  
|commit_csn|**bigint**|O número de sequência de confirmação específico da instância para a transação.|  
|commit_time|**smalldatetime**|A hora em que a transação foi confirmada.|  
|pdw_node_id|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="see-also"></a>Consulte Também  
 [Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Sobre o controle de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
  


