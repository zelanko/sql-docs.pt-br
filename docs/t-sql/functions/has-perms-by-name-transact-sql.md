---
description: HAS_PERMS_BY_NAME (Transact-SQL)
title: HAS_PERMS_BY_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HAS_PERMS_BY_NAME
- HAS_PERMS_BY_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], verifying
- current permission status
- checking permission status
- verifying permission status
- testing permissions
- HAS_PERMS_BY_NAME function
ms.assetid: eaf8cc82-1047-4144-9e77-0e1095df6143
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e2fa743ae09dc8a09a8edbc8e4a6e3b5cf8415db
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417342"
---
# <a name="has_perms_by_name-transact-sql"></a>HAS_PERMS_BY_NAME (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Avalia a permissão efetiva do usuário atual em um protegível. Uma função relacionada é [fn_my_permissions](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
HAS_PERMS_BY_NAME ( securable , securable_class , permission    
    [ , sub-securable ] [ , sub-securable_class ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *securable*  
 É o nome do protegível. Se o protegível for o próprio servidor, esse valor deverá ser definido como NULL. *securable* é uma expressão escalar do tipo **sysname**. Não há nenhum padrão.  
  
 *securable_class*  
 É o nome da classe do protegível na qual a permissão é testada. *securable_class* é uma expressão escalar do tipo **nvarchar(60)**.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], o argumento securable_class deve ser definido com um dos seguintes valores: **DATABASE**, **OBJECT**, **ROLE**, **SCHEMA** ou **USER**.  
  
 *permission*  
 Uma expressão escalar não nula do tipo **sysname** que representa o nome da permissão a ser verificado. Não há nenhum padrão. O nome da permissão ANY é um curinga.  
  
 *sub-securable*  
 Uma expressão escalar opcional do tipo **sysname** que representa o nome da subentidade protegível na qual a permissão é testada. O padrão é NULO.  
  
> [!NOTE]  
>  Nas versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e posteriores, os subprotegíveis não podem usar colchetes no formato **'[**_nome do subprotegível_**]'**. Em vez disso, use **'** _sub name_ **'** .  
  
 *sub-securable_class*  
 Uma expressão escalar opcional do tipo **nvarchar(60)** que representa a classe da subentidade protegível na qual a permissão é testada. O padrão é NULO.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], o argumento sub-securable_class apenas é válido se o argumento securable_class é definido como **OBJECT**. Se o argumento securable_class for definido como **OBJECT**, o argumento sub-securable_class deverá ser definido como **COLUMN**.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
 Retorna NULL quando a consulta falha.  
  
## <a name="remarks"></a>Comentários  
 Esta função interna testa se a entidade de segurança atual tem uma permissão efetiva específica em um protegível especificado. HAS_PERMS_BY_NAME retorna 1 quando o usuário tem permissão efetiva no protegível, 0 quando o usuário não tem nenhuma permissão efetiva no protegível e NULL quando a classe protegível ou permissão não é válida. Uma permissão efetiva é qualquer uma das permissões a seguir:  
  
-   Uma permissão concedida diretamente à entidade de segurança, e não negada.  
  
-   Uma permissão implicada por uma permissão de nível superior mantida pela entidade de segurança, e não negada.  
  
-   Uma permissão concedida a uma função ou grupo do qual a entidade de segurança é membro, e não negada.  
  
-   Uma permissão mantida por uma função ou grupo de qual a entidade de segurança é membro, e não negada.  
  
 A avaliação da permissão é sempre executada no contexto de segurança do chamador. Para determinar se algum outro usuário tem uma permissão efetiva, o chamador deve ter a permissão IMPERSONATE nesse usuário.  
  
 Para entidades em nível de esquema, nomes não nulos de uma, duas ou três partes são aceitos. Para entidades em nível de banco de dados, um nome de uma parte é aceito, com um valor nulo que significa “banco de dados atual”. Para o servidor propriamente dito, um valor nulo (que significa “servidor atual”) é obrigatório. Essa função não pode verificar permissões em um servidor vinculado ou em um usuário do Windows para o qual nenhuma entidade de segurança em nível de servidor tenha sido criada.  
  
 A consulta a seguir retornará uma lista de classes protegíveis internas:  
  
```  
SELECT class_desc FROM sys.fn_builtin_permissions(default);  
```  
  
 As ordenações a seguir são usadas:  
  
-   Ordenação do banco de dados atual: protegíveis em nível de banco de dados, incluindo protegíveis não contidos por um esquema, protegíveis com escopo no esquema de uma ou duas partes; banco de dados de destino quando um nome de três partes é usado.  
  
-   Ordenação do banco de dadosmaster: itens protegíveis do nível de servidor.  
  
-   Não há suporte para ‘ANY’ em verificações em nível de coluna. Você deve especificar a permissão apropriada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-do-i-have-the-server-level-view-server-state-permission"></a>a. Tenho a permissão VIEW SERVER STATE em nível de servidor?  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
```  
SELECT HAS_PERMS_BY_NAME(null, null, 'VIEW SERVER STATE');  
```  
  
### <a name="b-am-i-able-to-impersonate-server-principal-ps"></a>B. Posso executar IMPERSONATE na entidade de segurança do servidor Ps?  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
```  
SELECT HAS_PERMS_BY_NAME('Ps', 'LOGIN', 'IMPERSONATE');  
```  
  
### <a name="c-do-i-have-any-permissions-in-the-current-database"></a>C. Tenho alguma permissão no banco de dados atual?  
  
```  
SELECT HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'ANY');  
```  
  
### <a name="d-does-database-principal-pd-have-any-permission-in-the-current-database"></a>D. A entidade de segurança do banco de dados Pd tem alguma permissão no banco de dados atual?  
 Suponha que o chamador tenha a permissão IMPERSONATE na entidade de segurança `Pd`.  
  
```  
EXECUTE AS user = 'Pd'  
GO  
SELECT HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'ANY');  
GO  
REVERT;  
GO  
```  
  
### <a name="e-can-i-create-procedures-and-tables-in-schema-s"></a>E. Posso criar procedimentos e tabelas no esquema S?  
 O exemplo a seguir requer a permissão `ALTER` em `S` e a permissão `CREATE PROCEDURE` no banco de dados; de modo similar para tabelas.  
  
```  
SELECT HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'CREATE PROCEDURE')  
    & HAS_PERMS_BY_NAME('S', 'SCHEMA', 'ALTER') AS _can_create_procs,  
    HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'CREATE TABLE') &  
    HAS_PERMS_BY_NAME('S', 'SCHEMA', 'ALTER') AS _can_create_tables;  
```  
  
### <a name="f-which-tables-do-i-have-select-permission-on"></a>F. Em quais tabelas eu tenho a permissão SELECT?  
  
```  
SELECT HAS_PERMS_BY_NAME  
(QUOTENAME(SCHEMA_NAME(schema_id)) + '.' + QUOTENAME(name),   
    'OBJECT', 'SELECT') AS have_select, * FROM sys.tables  
```  
  
### <a name="g-do-i-have-insert-permission-on-the-salesperson-table-in-adventureworks2012"></a>G. Tenho a permissão INSERT na tabela SalesPerson no AdventureWorks2012?  
 O exemplo a seguir supõe que `AdventureWorks2012` é meu contexto de banco de dados atual e usa um nome de duas partes.  
  
```  
SELECT HAS_PERMS_BY_NAME('Sales.SalesPerson', 'OBJECT', 'INSERT');  
```  
  
 O exemplo a seguir não faz nenhuma suposição sobre meu contexto de banco de dados atual e usa um nome de três partes.  
  
```  
SELECT HAS_PERMS_BY_NAME('AdventureWorks2012.Sales.SalesPerson',   
    'OBJECT', 'INSERT');  
```  
  
### <a name="h-which-columns-of-table-t-do-i-have-select-permission-on"></a>H. Em quais colunas da tabela T eu tenho a permissão SELECT?  
  
```  
SELECT name AS column_name,   
    HAS_PERMS_BY_NAME('T', 'OBJECT', 'SELECT', name, 'COLUMN')   
    AS can_select   
    FROM sys.columns AS c   
    WHERE c.object_id=object_id('T');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [Hierarquia de permissões &#40;Mecanismo de banco de dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
  
  
