---
title: Permissões REVOKE do objeto do sistema (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statement, system objects
- permissions [SQL Server], system objects
ms.assetid: 84983238-dd7d-45bd-99bb-52c9d8e96a87
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 47428ffc2ab1074ec2b4ce1789e679c184607a05
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67914211"
---
# <a name="revoke-system-object-permissions-transact-sql"></a>Permissões de objeto do sistema REVOKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Revoga permissões em objetos de sistema como procedimentos armazenados, procedimentos armazenados estendidos, funções e exibições de um principal.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
REVOKE { SELECT | EXECUTE } ON [sys.]system_object FROM principal   
```  
  
## <a name="arguments"></a>Argumentos  
 [**sys.** ] .  
 O qualificador **sys** só é necessário quando você está referenciando exibições do catálogo e exibições de gerenciamento dinâmico.  
  
 *system_object*  
 Especifica o objeto no qual a permissão está sendo revogada.  
  
 *principal*  
 Especifica a entidade a partir da qual a permissão está sendo revogada.  
  
## <a name="remarks"></a>Comentários  
 Essa instrução pode ser usada para revogar permissões em determinados procedimentos armazenados, procedimentos armazenados estendidos, funções com valor de tabela, funções escalares, exibições, exibições do catálogo, exibições de compatibilidade, exibições INFORMATION_SCHEMA, exibições de gerenciamento dinâmico e tabelas de sistema instaladas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para cada um desses objetos de sistema, existe como um registro exclusivo no banco de dados de recursos (**mssqlsystemresource**). O banco de dados de recursos é somente leitura. Um link para o objeto é exposto como um registro no esquema **sys** de todo banco de dados.  
  
 A resolução de nome padrão resolve nomes de procedimento não qualificados para o banco de dados de recursos. Portanto, o qualificador **sys.** é necessário somente ao especificar exibições do catálogo e exibições de gerenciamento dinâmico.  
  
> [!CAUTION]  
>  A revogação de permissões em objetos do sistema provocará falha nos aplicativos que dependem deles. O [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usa exibições do catálogo e pode não funcionar como o esperado se você alterar as permissões padrão em exibições do catálogo.  
  
 A revogação de permissões em gatilhos e em colunas de objetos de sistema não possui suporte.  
  
 As permissões em objetos do sistema serão preservadas nas atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Os objetos do sistema são visíveis na exibição de catálogo [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) .  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir revoga a permissão `EXECUTE` no `sp_addlinkedserver` a partir de `public`.  
  
```  
REVOKE EXECUTE ON sys.sp_addlinkedserver FROM public;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys.system_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [Permissões GRANT do Objeto do Sistema &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)   
 [Permissões DENY de objeto do sistema &#40;Transact-SQL&#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)  
  
  
