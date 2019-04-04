---
title: sys.fn_PageResCracker (Transact-SQL) | Microsoft Docs
description: Documentação para a função de sistema sys.fn_PageResCracker.
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
ms.openlocfilehash: 2fc7136b60dba47813b9942316ee6fdfbc64f307
ms.sourcegitcommit: fc1739be9b2735b2bb469979936e76ca2a3830f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2019
ms.locfileid: "58899702"
---
# <a name="sysfnpagerescracker-transact-sql"></a>sys.fn_PageResCracker (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Retorna o `db_id`, `file_id`, e `page_id` para o determinado `page_resource` valor. 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
```  
sys.fn_PageResCracker ( page_resource )  
```  
  
## <a name="arguments"></a>Argumentos  
*page_resource*    
É o formato hexadecimal de 8 bytes de um recurso de página do banco de dados.
  
## <a name="tables-returned"></a>Tabelas retornadas  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|db_id|**INT**|ID do banco de dados|  
|file_id|**INT**|ID do Arquivo|  
|page_id|**INT**|ID da página|  
  
## <a name="remarks"></a>Comentários  
`sys.fn_PageResCracker` é usado para converter a representação hexadecimal de 8 bytes de uma página de banco de dados em um conjunto de linhas que contém a ID de banco de dados, o arquivo de ID e a ID de página da página.   

Você pode obter um recurso de página válidos do `page_resource` coluna do [. DM exec_requests &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) exibição de gerenciamento dinâmico ou a [sys. sysprocesses &#40;&#41; ](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md) exibição do sistema. Se um recurso de página inválida for usado, em seguida, o retorno será NULL.  
O principal uso de `sys.fn_PageResCracker` é facilitar as uniões entre esses modos de exibição e o [sys.dm_db_page_info &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) função de gerenciamento dinâmico para obter informações sobre a página, como o objeto ao qual ele pertence.
  
## <a name="permissions"></a>Permissões  
O usuário precisa `VIEW SERVER STATE` permissão no servidor.  
  
## <a name="examples"></a>Exemplos  
O `sys.fn_PageResCracker` função pode ser usada em conjunto com [sys.dm_db_page_info &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) solucionar problemas de página relacionado esperas e bloqueio nas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  O script a seguir é um exemplo de como você pode usar essas funções para coletar informações de página do banco de dados para todas as solicitações ativas que estão aguardando em algum tipo de recurso da página. 
  
```sql  
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 1) AS page_info
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_db_page_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)  
 [sys.sysprocesses &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
