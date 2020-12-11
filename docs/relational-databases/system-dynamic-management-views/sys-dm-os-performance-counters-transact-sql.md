---
description: sys.dm_os_performance_counters (Transact-SQL)
title: sys.dm_os_performance_counters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_performance_counters
- sys.dm_os_performance_counters_TSQL
- dm_os_performance_counters_TSQL
- sys.dm_os_performance_counters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_performance_counters dynamic management view
ms.assetid: a1c3e892-cd48-40d4-b6be-2a9246e8fbff
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4b60b8b79eb5b325760c9058c4e252dc45b0e895
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97325817"
---
# <a name="sysdm_os_performance_counters-transact-sql"></a>sys.dm_os_performance_counters (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna uma linha por contador de desempenho mantido pelo servidor. Para obter informações sobre cada contador de desempenho, consulte [usar objetos de SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md).  
  
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys.dm_pdw_nodes_os_performance_counters**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|Categoria para a qual este contador pertence.|  
|**counter_name**|**nchar(128)**|Nome do contador. Para obter mais informações sobre um contador, este é o nome do tópico a ser selecionado na lista de contadores em [usar SQL Server objetos](../../relational-databases/performance-monitor/use-sql-server-objects.md). |  
|**instance_name**|**nchar(128)**|Nome da instância específica do contador. Normalmente, contém o nome do banco de dados.|  
|**cntr_value**|**bigint**|Valor atual do contador.<br /><br /> **Observação:** Para contadores por segundo, esse valor é cumulativo. O valor de taxa deve ser calculado pela amostragem do valor a intervalos de tempo curtos. A diferença entre qualquer dois valores de amostra sucessivos é igual à taxa para o intervalo de tempo usado.|  
|**cntr_type**|**int**|Tipo de contador conforme definido pela arquitetura de desempenho do Windows. Consulte [tipos de contador de desempenho WMI](/windows/desktop/WmiSdk/wmi-performance-counter-types) em documentos ou a documentação do Windows Server para obter mais informações sobre os tipos de contador de desempenho.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="remarks"></a>Comentários  
 Se a instância da instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não conseguir exibir os contadores de desempenho do sistema operacional Windows, use a seguinte consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] para confirmar se os contadores de desempenho foram desabilitados.  
  
```sql  
SELECT COUNT(*) FROM sys.dm_os_performance_counters;  
```  
  
Se o valor de retorno for 0 linha, significa que os contadores de desempenho foram desabilitados. Em seguida, você deve examinar o log de instalação e procurar o erro 3409, `Reinstall sqlctr.ini for this instance, and ensure that the instance login account has correct registry permissions.` isso indica que os contadores de desempenho não foram habilitados. Os erros imediatamente antes do erro 3409 devem indicar a causa da falha na habilitação dos contadores de desempenho. Para obter mais informações sobre os arquivos de log da instalação, consulte [Exibir e ler SQL Server arquivos de log da instalação](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  

Os contadores de desempenho em que o `cntr_type` valor da coluna é 65792, 272696320 e 537003264 exibem um valor de contador de instantâneo imediato.

Contadores de desempenho em que o `cntr_type` valor da coluna é 272696576, 1073874176 e 1073939712 exibem valores de contador cumulativo em vez de um instantâneo instantâneo. Dessa forma, para obter uma leitura do tipo instantâneo, você deve comparar o Delta entre dois pontos de coleta.

## <a name="permission"></a>Permissão

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nos objetivos do serviço básico, S0 e S1 do banco de dados SQL, e para bancos de dados em pools elásticos, o `Server admin` ou uma `Azure Active Directory admin` conta é necessária. Em todos os outros objetivos de serviço do banco de dados SQL, a `VIEW DATABASE STATE` permissão é necessária no banco de dados.   
 
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os contadores de desempenho que exibem valores de contador de instantâneo.  
  
```sql  
SELECT object_name, counter_name, instance_name, cntr_value, cntr_type  
FROM sys.dm_os_performance_counters
WHERE cntr_type = 65792 OR cntr_type = 272696320 OR cntr_type = 537003264;  
```  
  
## <a name="see-also"></a>Consulte Também  
  [SQL Server exibições de gerenciamento dinâmico relacionadas ao sistema operacional &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
