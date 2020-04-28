---
title: sys. security_predicates (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.SECURITY_PREDICATES
- SECURITY_PREDICATES
- SECURITY_PREDICATES_TSQL
- SYS.SECURITY_PREDICATES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.security_predicates catalog view
- security_predicates catalog view
ms.assetid: c7a2f28c-98da-463d-8b8a-8e5619e2c6a6
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6cf464370c5c2ca3f5075205c6783e9332309f12
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68135219"
---
# <a name="syssecurity_predicates-transact-sql"></a>sys. security_predicates (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Retorna uma linha para cada predicado de segurança no banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|object_id|**int**|ID da política de segurança que contém esse predicado.|  
|security_predicate_id|**int**|ID do predicado nesta política de segurança.|  
|target_object_id|**int**|ID do objeto no qual o predicado de segurança está associado.|  
|predicate_definition|**nvarchar(max)**|Nome totalmente qualificado da função que será usada como um predicado de segurança, incluindo os argumentos. Observe que o nome `schema.function` pode ser normalizado (ou seja, escrito com caracteres de escape), bem como qualquer outro elemento em texto para manter a consistência. Por exemplo:<br /><br /> `[dbo].[fn_securitypredicate]([wing], [startTime], [endTime])`|  
|predicate_type|**int**|O tipo de predicado usado pela política de segurança:<br /><br /> 0 = PREDICADO DE FILTRO<br /><br /> 1 = PREDICADO DE BLOQUEIO|  
|predicate_type_desc|**nvarchar(60)**|O tipo de predicado usado pela política de segurança:<br /><br /> FILTER<br /><br /> BLOQUEAR|  
|operação|**int**|O tipo de operação especificado para o predicado:<br /><br /> NULL = todas as operações aplicáveis<br /><br /> 1 = APÓS INSERIR<br /><br /> 2 = APÓS A ATUALIZAÇÃO<br /><br /> 3 = ANTES DA ATUALIZAÇÃO<br /><br /> 4 = ANTES DA EXCLUSÃO|  
|operation_desc|**nvarchar(60)**|O tipo de operação especificado para o predicado:<br /><br /> NULO<br /><br /> APÓS A INSERÇÃO<br /><br /> AFTER UPDATE<br /><br /> ANTES DA ATUALIZAÇÃO<br /><br /> ANTES DA EXCLUSÃO|  
  
## <a name="permissions"></a>Permissões  
 Entidades com a permissão **alterar qualquer política de segurança** têm acesso a todos os objetos nessa exibição de catálogo, bem como a qualquer pessoa com **definição de exibição** no objeto.  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança em nível de linha](../../relational-databases/security/row-level-security.md)   
 [sys. security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [CRIAR política de segurança &#40;&#41;Transact-SQL](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [Exibições do catálogo de segurança &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
