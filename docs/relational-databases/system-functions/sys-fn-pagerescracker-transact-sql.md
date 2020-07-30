---
title: sys. fn_PageResCracker (Transact-SQL) | Microsoft Docs
description: Saiba mais sobre a função de sistema sys. fn_PageResCracker. Veja exemplos e exiba recursos adicionais disponíveis.
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_PageResCracker
- sys.fn_PageResCracker_TSQL
- fn_PageResCracker_TSQL
- sys.fn_PageResCracker
- sys.dm_db_page_info
dev_langs:
- TSQL
helpviewer_keywords:
- fn_PageResCracker function
- page_resource
- sys.fn_PageResCracker function
- sys.dm_db_page_info
- page info
author: bluefooted
ms.author: pamela
manager: amitban
ms.openlocfilehash: a48b5ba06223130a83980bf6cf8ec410bd58e5a1
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247575"
---
# <a name="sysfn_pagerescracker-transact-sql"></a>sys. fn_PageResCracker (Transact-SQL)
[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

Retorna o `db_id` , `file_id` e `page_id` para o valor especificado `page_resource` . 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
```  
sys.fn_PageResCracker ( page_resource )  
```  
  
## <a name="arguments"></a>Argumentos  
*page_resource*    
É o formato hexadecimal de 8 bytes de um recurso de página de banco de dados.
  
## <a name="tables-returned"></a>Tabelas retornadas  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|db_id|**int**|ID do banco de dados|  
|file_id|**int**|ID do Arquivo|  
|page_id|**int**|ID da página|  
  
## <a name="remarks"></a>Comentários  
`sys.fn_PageResCracker`é usado para converter a representação hexadecimal de 8 bytes de uma página de banco de dados em um conjunto de linhas que contém a ID do banco de dados, a ID de arquivo e a ID de página da página.   

Você pode obter um recurso de página válido a partir da `page_resource` coluna da exibição de gerenciamento dinâmico de [Dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) ou dos processos desys.sys&#40;exibição do sistema [Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md) . Se um recurso de página inválido for usado, o retorno será nulo.  
O principal uso do `sys.fn_PageResCracker` é facilitar as junções entre essas exibições e o [sys. dm_db_page_info &#40;função de gerenciamento dinâmico&#41;TRANSACT-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) para obter informações sobre a página, como o objeto ao qual ela pertence.
  
## <a name="permissions"></a>Permissões  
O usuário precisa de `VIEW SERVER STATE` permissão no servidor.  
  
## <a name="examples"></a>Exemplos  
A `sys.fn_PageResCracker` função pode ser usada em conjunto com [sys. Dm_db_page_info &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) para solucionar problemas de esperas e bloqueios relacionados à página no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  O script a seguir é um exemplo de como você pode usar essas funções para coletar informações de página de banco de dados para todas as solicitações ativas que estão aguardando no momento algum tipo de recurso de página. 
  
```sql  
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 1) AS page_info
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys. dm_db_page_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)  
 [Processos desys.sys&#40;&#41;de Transact-SQL](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
