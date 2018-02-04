---
title: sys.fn_my_permissions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fn_my_permissions_TSQL
- fn_my_permissions_TSQL
- sys.fn_my_permissions
- fn_my_permissions
dev_langs:
- TSQL
helpviewer_keywords:
- fn_my_permissions function
- sys.fn_my_permissions function
ms.assetid: 30f97f00-03d8-443a-9de9-9ec420b7699b
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: craigg
ms.workload: Active
ms.openlocfilehash: 9eb23a2de7fda489b205f1eaf89c124068be63b3
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysfnmypermissions-transact-sql"></a>sys.fn_my_permissions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma lista das permissões efetivamente concedidas à entidade em um protegível. Uma função relacionada é [HAS_PERMS_BY_NAME](../../t-sql/functions/has-perms-by-name-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn_my_permissions ( securable , 'securable_class' )  
```  
  
## <a name="arguments"></a>Argumentos  
 *securable*  
 É o nome do protegível. Se o protegível for o servidor ou um banco de dados, esse valor deverá ser definido como NULL. *protegível* é uma expressão escalar do tipo **sysname**. *protegível* pode ser um nome com diversas partes.  
  
 '*securable_class*'  
 É o nome da classe de protegível para a qual são listadas as permissões. *securable_class* é um **sysname**. *securable_class* deve ser um dos seguintes: função de aplicativo, ASSEMBLY, chave ASSIMÉTRICA, certificado, contrato, banco de dados, ponto de EXTREMIDADE, FULLTEXT CATALOG, LOGIN, tipo de mensagem, objeto, REMOTE SERVICE BINDING, função, ROTA, esquema, servidor, serviço , CHAVE SIMÉTRICA, TIPO, USUÁRIO, COLEÇÃO DE ESQUEMAS XML.  
  
## <a name="columns-returned"></a>Colunas retornadas  
 A tabela a seguir lista as colunas que **fn_my_permissions** retorna. Cada linha retornada descreve uma permissão mantida pelo contexto de segurança atual no protegível. Retorna NULL se a consulta falhar.  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|entity_name|**sysname**|Nome do protegível no qual as permissões listadas são efetivamente concedidas.|  
|subentity_name|**sysname**|Nome da coluna se o protegível tiver colunas; caso contrário, será NULL.|  
|permission_name|**nvarchar**|Nome da permissão.|  
  
## <a name="remarks"></a>Remarks  
 Esta função com valor de tabela retorna uma lista das permissões efetivas mantidas pela entidade de chamada em um protegível especificado. Uma permissão efetiva é qualquer uma das seguintes:  
  
-   Uma permissão concedida diretamente à entidade de segurança, e não negada.  
  
-   Uma permissão implicada por uma permissão de nível superior mantida pela entidade de segurança, e não negada.  
  
-   Uma permissão concedida a uma função ou grupo do qual a entidade de segurança é membro, e não negada.  
  
-   Uma permissão mantida por uma função ou grupo de qual a entidade de segurança é membro, e não negada.  
  
 A avaliação da permissão é sempre executada no contexto de segurança do chamador. Para determinar se alguma outra entidade tem uma permissão efetiva, o chamador deve ter a permissão IMPERSONATE nessa entidade.  
  
 Para entidades em nível de esquema, nomes não nulos de uma, duas ou três partes são aceitos. Para entidades de nível de banco de dados, um nome de uma parte é aceito, com uma valor nulo que significa "*banco de dados atual*". Para o servidor propriamente dito, um valor nulo (que significa “servidor atual”) é obrigatório. **fn_my_permissions** não é possível verificar as permissões em um servidor vinculado.  
  
 A consulta a seguir retornará uma lista de classes protegíveis internas:  
  
```  
SELECT DISTINCT class_desc FROM fn_builtin_permissions(default)  
    ORDER BY class_desc;  
GO  
```  
  
 Se o padrão é fornecido como o valor de *protegível* ou *securable_class*, o valor será interpretado como NULL.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-effective-permissions-on-the-server"></a>A. Listando permissões efetivas no servidor  
 O exemplo a seguir retorna uma lista de permissões efetivas do chamador no servidor.  
  
```  
SELECT * FROM fn_my_permissions(NULL, 'SERVER');  
GO  
```  
  
### <a name="b-listing-effective-permissions-on-the-database"></a>B. Listando permissões efetivas no banco de dados  
 O exemplo a seguir retorna uma lista de permissões efetivas do chamador no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE AdventureWorks2012;  
SELECT * FROM fn_my_permissions (NULL, 'DATABASE');  
GO  
```  
  
### <a name="c-listing-effective-permissions-on-a-view"></a>C. Listando permissões efetivas em uma exibição  
 O exemplo a seguir retorna uma lista de permissões efetivas do chamador na exibição `vIndividualCustomer` no esquema `Sales` do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE AdventureWorks2012;  
SELECT * FROM fn_my_permissions('Sales.vIndividualCustomer', 'OBJECT')   
    ORDER BY subentity_name, permission_name ;   
GO   
```  
  
### <a name="d-listing-effective-permissions-of-another-user"></a>D. Listando permissões efetivas de outro usuário  
 O exemplo a seguir retorna uma lista de permissões efetivas do usuário de banco de dados `Wanida` na tabela `Employee` no esquema `HumanResources` do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. O chamador requer a permissão IMPERSONATE no usuário `Wanida`.  
  
```  
EXECUTE AS USER = 'Wanida';  
SELECT * FROM fn_my_permissions('HumanResources.Employee', 'OBJECT')   
    ORDER BY subentity_name, permission_name ;    
REVERT;  
GO  
```  
  
### <a name="e-listing-effective-permissions-on-a-certificate"></a>E. Listando permissões efetivas em um certificado  
 O exemplo a seguir retorna uma lista das permissões efetivas do chamador em um certificado denominado `Shipping47` no banco de dados atual.  
  
```  
SELECT * FROM fn_my_permissions('Shipping47', 'CERTIFICATE');  
GO  
```  
  
### <a name="f-listing-effective-permissions-on-an-xml-schema-collection"></a>F. Listando permissões efetivas em uma coleção de esquemas XML  
 O exemplo a seguir retorna uma lista das permissões efetivas do chamador em uma coleção de esquema XML chamado `ProductDescriptionSchemaCollection` no [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] banco de dados.  
  
```  
USE AdventureWorks2012;  
SELECT * FROM fn_my_permissions('ProductDescriptionSchemaCollection',  
    'XML SCHEMA COLLECTION');  
GO  
```  
  
### <a name="g-listing-effective-permissions-on-a-database-user"></a>G. Listando permissões efetivas em um usuário de banco de dados  
 O exemplo a seguir retorna uma lista das permissões efetivas do chamador em um usuário denominado `MalikAr` no banco de dados atual.  
  
```  
SELECT * FROM fn_my_permissions('MalikAr', 'USER');  
GO  
```  
  
### <a name="h-listing-effective-permissions-of-another-login"></a>H. Listando permissões efetivas de outro logon  
 O exemplo a seguir retorna uma lista de permissões efetivas do logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `WanidaBenshoof` na tabela `Employee` no esquema `HumanResources`do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. O chamador requer a permissão IMPERSONATE no logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `WanidaBenshoof`.  
  
```  
EXECUTE AS LOGIN = 'WanidaBenshoof';  
SELECT * FROM fn_my_permissions('AdventureWorks2012.HumanResources.Employee', 'OBJECT')   
    ORDER BY subentity_name, permission_name ;    
REVERT;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [Hierarquia de permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  
