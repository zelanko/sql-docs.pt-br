---
title: sys. fn_PageResCracker (Transact-SQL) | Microsoft Docs
description: Documentação da função de sistema sys. fn_PageResCracker.
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
ms.openlocfilehash: 6d8203979a0afdca1ae78b9bd51723c906c40ea2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68267069"
---
# <a name="sysfn_pagerescracker-transact-sql"></a>sys. fn_PageResCracker (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Retorna o `db_id`, `file_id`e `page_id` para o valor especificado `page_resource` . 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
```  
sys.fn_PageResCracker ( page_resource )  
```  
  
## <a name="arguments"></a>Argumentos  
*page_resource*    
É o formato hexadecimal de 8 bytes de um recurso de página de banco de dados.
  
## <a name="tables-returned"></a>Tabelas retornadas  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|db_id|**int**|ID do banco de dados|  
|file_id|**int**|ID do Arquivo|  
|page_id|**int**|ID da página|  
  
## <a name="remarks"></a>Comentários  
`sys.fn_PageResCracker`é usado para converter a representação hexadecimal de 8 bytes de uma página de banco de dados em um conjunto de linhas que contém a ID do banco de dados, a ID de arquivo e a ID de página da página.   

Você pode obter um recurso de página válido a `page_resource` partir da coluna da exibição dm_exec_requests de gerenciamento dinâmico do sysprocesses [&#40;TRANSACT-&#41;SQL](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) ou do modo de exibição do sistema [Transact-SQL&#41;&#40;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md) . Se um recurso de página inválido for usado, o retorno será nulo.  
O principal uso do `sys.fn_PageResCracker` é facilitar as junções entre essas exibições e o [sys. dm_db_page_info &#40;função de gerenciamento dinâmico&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) para obter informações sobre a página, como o objeto ao qual ela pertence.
  
## <a name="permissions"></a>Permissões  
O usuário precisa `VIEW SERVER STATE` de permissão no servidor.  
  
## <a name="examples"></a>Exemplos  
A `sys.fn_PageResCracker` função pode ser usada em conjunto com [sys. dm_db_page_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) para solucionar problemas de esperas e bloqueios relacionados à página no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  O script a seguir é um exemplo de como você pode usar essas funções para coletar informações de página de banco de dados para todas as solicitações ativas que estão aguardando no momento algum tipo de recurso de página. 
  
```sql  
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 1) AS page_info
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys. dm_db_page_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)  
 [sys. sysprocesses &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
