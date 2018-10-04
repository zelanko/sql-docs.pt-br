---
title: procedimento sp_addextendedproperty (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropextendedproperty_TSQL
- sp_dropextendedproperty
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropextendedproperty
ms.assetid: 4851865a-86ca-4823-991a-182dd1934075
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7e01b14407198ed88654527bd247a116c200fb1e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47627424"
---
# <a name="spdropextendedproperty-transact-sql"></a>sp_dropextendedproperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Descarta uma propriedade estendida existente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropextendedproperty   
    [ @name = ] { 'property_name' }  
      [ , [ @level0type = ] { 'level0_object_type' }   
        , [ @level0name = ] { 'level0_object_name' }   
            [ , [ @level1type = ] { 'level1_object_type' }   
              , [ @level1name = ] { 'level1_object_name' }   
                [ , [ @level2type = ] { 'level2_object_type' }   
                  , [ @level2name = ] { 'level2_object_name' }   
                ]   
            ]   
        ]   
    ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [ @name=] {'*property_name*'}  
 É o nome da propriedade a ser removida. *Property_Name* está **sysname** e não pode ser NULL.  
  
 [ @level0type=] {'*level0_object_type*'}  
 É o nome do tipo de objeto de nível 0 especificado. *level0_object_type* está **varchar (128)**, com um padrão NULL.  
  
 As entradas válidas são ASSEMBLY, CONTRACT, EVENT NOTIFICATION, FILEGROUP, MESSAGE TYPE, PARTITION FUNCTION, PARTITION SCHEME, REMOTE SERVICE BINDING, ROUTE, SCHEMA, SERVICE, USER, TRIGGER, TYPE e NULL.  
  
> [!IMPORTANT]  
>  USER e TYPE como tipos de nível 0 serão removidos em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esses recursos em novo trabalho de desenvolvimento e planeje modificar os aplicativos que os usam atualmente. Use SCHEMA como o tipo de nível 0 em vez de USER. Para TYPE, use SCHEMA como o tipo de nível 0 e TYPE como o tipo de nível 1.  
  
 [ @level0name=] {'*level0_object_name*'}  
 É o nome do tipo de objeto de nível 0 especificado. *level0_object_name* está **sysname** com um padrão NULL.  
  
 [ @level1type=] {'*level1_object_type*'}  
 É o tipo de objeto de nível 1. *level1_object_type* está **varchar (128)** com um padrão NULL. As entradas válidas são AGGREGATE, DEFAULT, FUNCTION, LOGICAL FILE NAME, PROCEDURE, QUEUE, RULE, SYNONYM, TABLE, TABLE_TYPE, TYPE, VIEW, XML SCHEMA COLLECTION e NULL.  
  
 [ @level1name=] {'*level1_object_name*'}  
 É o nome do tipo de objeto de nível 1 especificado. *level1_object_name* está **sysname** com um padrão NULL.  
  
 [ @level2type=] {'*level2_object_type*'}  
 É o tipo de objeto de nível 2. *level2_object_type* está **varchar (128)** com um padrão NULL. As entradas válidas são COLUMN, CONSTRAINT, EVENT NOTIFICATION, INDEX, PARAMETER, TRIGGER e NULL.  
  
 [ @level2name=] {'*level2_object_name*'}  
 É o nome do tipo de objeto de nível 2 especificado. *level2_object_name* está **sysname** com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Com o propósito de especificar as propriedades estendidas, os objetos em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são classificados em três níveis: 0, 1 e 2. O nível 0 é o mais alto e é definido como objetos que estão contidos no escopo do banco de dados. Os objetos de nível 1 estão contidos em um esquema ou escopo de usuário e os objetos de nível 2 estão contidos pelos objetos de nível 1. As propriedades estendidas podem ser definidas para os objetos em qualquer um desses níveis. As referências a um objeto de um nível precisam ser qualificadas com os tipos e os nomes de todos os objetos de nível.  
  
 Dado um válido *property_name*, se todos os tipos de objeto e os nomes forem nulos e a propriedade existir no banco de dados atual, essa propriedade será excluída. Veja o exemplo B a seguir, após este tópico.  
  
## <a name="permissions"></a>Permissões  
 Os membros das funções de banco de dados fixa db_owner e db_ddladmin podem descartar propriedades estendidas de qualquer objeto com a seguinte exceção: db_ddladmin não pode adicionar propriedades ao banco de dados em si ou a usuários ou funções.  
  
 Os usuários podem descartar as propriedades estendidas para os objetos que possuírem ou para os quais tenham as permissões ALTER ou CONTROL.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-dropping-an-extended-property-on-a-column"></a>A. Removendo uma propriedade estendida em uma coluna  
 O exemplo a seguir remove a propriedade `caption` da coluna `id` na tabela `T1` contida no esquema `dbo`.  
  
```  
CREATE TABLE T1 (id int , name char (20));  
GO  
EXEC sp_addextendedproperty   
     @name = 'caption'   
    ,@value = 'Employee ID'   
    ,@level0type = 'schema'   
    ,@level0name = dbo  
    ,@level1type = 'table'  
    ,@level1name = 'T1'  
    ,@level2type = 'column'  
    ,@level2name = id;  
GO  
EXEC sp_dropextendedproperty   
     @name = 'caption'   
    ,@level0type = 'schema'   
    ,@level0name = dbo  
    ,@level1type = 'table'  
    ,@level1name = 'T1'  
    ,@level2type = 'column'  
    ,@level2name = id;  
GO  
DROP TABLE T1;  
GO  
```  
  
### <a name="b-dropping-an-extended-property-on-a-database"></a>B. Removendo uma propriedade estendida em um banco de dados  
 O exemplo a seguir remove a propriedade chamada `MS_Description` do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] banco de dados de exemplo. Como a propriedade está no banco de dados em si, nenhum tipo de objeto e nome é especificado.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_dropextendedproperty   
@name = N'MS_Description';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys.fn_listextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [sp_addextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [sp_updateextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updateextendedproperty-transact-sql.md)   
 [sys.extended_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)  
  
  
