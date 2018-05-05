---
title: sys.dm_tran_top_version_generators (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_tran_top_version_generators
- sys.dm_tran_top_version_generators
- dm_tran_top_version_generators_TSQL
- sys.dm_tran_top_version_generators_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_top_version_generators dynamic management view
ms.assetid: cec7809b-ba8a-4df9-b5bb-d4f651ff1a86
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f0775e69eee7403f7e4f960a2b658dd3416d0d83
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmtrantopversiongenerators-transact-sql"></a>sys.dm_tran_top_version_generators (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma tabela virtual para os objetos que estão produzindo a maioria das versões no repositório de versão. **sys.DM tran_top_version_generators** retorna os maiores 256 agregados tamanhos de registros são agrupados pelo **database_id** e **rowset_id**. **sys.DM tran_top_version_generators** recupera dados consultando a **dm_tran_version_store** tabela virtual. **sys.DM tran_top_version_generators** é uma exibição ineficiente para execução porque essa exibição consulta todo o armazenamento de versão e o armazenamento de versão pode ser muito grande. Recomendados que você use essa função para localizar os usuários que mais utilizam o armazenamento de versão.  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_tran_top_version_generators**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.dm_tran_top_version_generators  
```  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**Int**|ID do banco de dados.|  
|**rowset_id**|**bigint**|ID do conjunto de linhas.|  
|**aggregated_record_length_in_bytes**|**Int**|Soma dos comprimentos de registro para cada **database_id** e **rowset_id pair** no repositório de versão.|  
|**pdw_node_id**|**Int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   

## <a name="remarks"></a>Remarks  
 Porque **sys.DM tran_top_version_generators** talvez precise ler muitas páginas enquanto examina o repositório de versão, executando **sys.DM tran_top_version_generators** podem interferir no sistema desempenho.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa um cenário de teste no qual quatro transações simultâneas, cada uma identificada por um XSN (número de sequência de transação), estão sendo executadas em um banco de dados no qual as opções ALLOW_SNAPSHOT_ISOLATION e READ_COMMITTED_SNAPSHOT estão definidas como ON. As seguintes transações estão sendo executadas:  
  
-   XSN-57 é uma operação de atualização sob o isolamento serializável.  
  
-   XSN-58 é o mesmo que XSN-57.  
  
-   XSN-59 é uma operação de seleção em isolamento de instantâneo.  
  
-   XSN-60 é o mesmo que XSN-59.  
  
 A consulta a seguir é executada.  
  
```  
SELECT  
    database_id,  
    rowset_id,  
    aggregated_record_length_in_bytes  
  FROM sys.dm_tran_top_version_generators;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
database_id rowset_id            aggregated_record_length_in_bytes  
----------- -------------------- ---------------------------------  
9           72057594038321152    87  
9           72057594038386688    33  
```  
  
 A saída mostra que todas as versões são criadas por `database_id``9` e que geram as versões de duas tabelas.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à transação &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


