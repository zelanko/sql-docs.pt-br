---
title: sys.DM os_performance_counters (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_os_performance_counters
- sys.dm_os_performance_counters_TSQL
- dm_os_performance_counters_TSQL
- sys.dm_os_performance_counters
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_performance_counters dynamic management view
ms.assetid: a1c3e892-cd48-40d4-b6be-2a9246e8fbff
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e0251869bd6dc3fb3ef39b5aebb31af346648b2d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosperformancecounters-transact-sql"></a>sys.dm_os_performance_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Retorna uma linha por contador de desempenho mantido pelo servidor. Para obter informações sobre cada contador de desempenho, consulte [usar objetos do SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md).  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_performance_counters**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|Categoria para a qual este contador pertence.|  
|**counter_name**|**nchar(128)**|Nome do contador. Para obter mais informações sobre um contador, esse é o nome do tópico para selecionar na lista de contadores no [usar objetos do SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md). |  
|**nome_da_instância**|**nchar(128)**|Nome da instância específica do contador. Normalmente, contém o nome do banco de dados.|  
|**cntr_value**|**bigint**|Valor atual do contador.<br /><br /> **Observação:** para contadores por segundo, esse valor é cumulativo. O valor de taxa deve ser calculado pela amostragem do valor a intervalos de tempo curtos. A diferença entre qualquer dois valores de amostra sucessivos é igual à taxa para o intervalo de tempo usado.|  
|**cntr_type**|**int**|Tipo de contador conforme definido pela arquitetura de desempenho do Windows. Consulte [tipos de contador de desempenho WMI](http://msdn2.microsoft.com/library/aa394569.aspx) no MSDN ou a documentação do Windows Server para obter mais informações sobre tipos de contador de desempenho.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="remarks"></a>Comentários  
 Se a instância da instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não conseguir exibir os contadores de desempenho do sistema operacional Windows, use a seguinte consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] para confirmar se os contadores de desempenho foram desabilitados.  
  
```  
SELECT COUNT(*) FROM sys.dm_os_performance_counters;  
```  
  
 Se o valor de retorno for 0 linha, significa que os contadores de desempenho foram desabilitados. Você deve analisar o log da instalação e procurar o erro 3409, "Reinstale o arquivo sqlctr.ini nessa instância e verifique se a conta de logon da instância tem permissões corretas de Registro".  Ele indica que os contadores de desempenho não foram habilitados. Os erros imediatamente antes do erro 3409 devem indicar a causa da falha na habilitação dos contadores de desempenho. Para obter mais informações sobre os arquivos de log de instalação, consulte [exibir e ler arquivos de Log do SQL Server Setup](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
## <a name="permission"></a>Permissão  
Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, requer o `VIEW DATABASE STATE` no banco de dados. Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, requer o **administrador do servidor** ou um **administrador do Active Directory do Azure** conta.    
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna valores de contador de desempenho.  
  
```  
SELECT object_name, counter_name, instance_name, cntr_value, cntr_type  
FROM sys.dm_os_performance_counters;  
  
```  
  
## <a name="see-also"></a>Consulte também  
  [Sistema operacional SQL Server relacionadas exibições de gerenciamento dinâmico &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  


