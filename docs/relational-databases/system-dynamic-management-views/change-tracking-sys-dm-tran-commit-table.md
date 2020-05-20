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
ms.openlocfilehash: 84278124664b72c45e038de7981057eaff1014f0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82819719"
---
# <a name="change-tracking---sysdm_tran_commit_table"></a>Controle de Alterações-sys. dm_tran_commit_table
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

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
  
  


