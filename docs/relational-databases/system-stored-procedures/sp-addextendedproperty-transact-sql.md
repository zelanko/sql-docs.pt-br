---
description: sp_addextendedproperty (Transact-SQL)
title: sp_addextendedproperty (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addextendedproperty
- sp_addextendedproperty_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addextendedproperty
ms.assetid: 565483ea-875b-4133-b327-d0006d2d7b4c
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 184328e9b6d5c197b06f89f151942535a90f7f91
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474647"
---
# <a name="sp_addextendedproperty-transact-sql"></a>sp_addextendedproperty (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Adiciona uma nova propriedade estendida a um objeto de banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addextendedproperty  
    [ @name = ] { 'property_name' }  
    [ , [ @value = ] { 'value' }   
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
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @name ] = {'*property_name*'}  
 É o nome da propriedade a ser adicionada. *property_name* é **sysname** e não pode ser nulo. Os nomes também podem incluir espaço em branco ou cadeias de caracteres não alfanuméricos e valores binários.  
  
 [ @value =] {'*valor*'}  
 É o valor a ser associado à propriedade. o *valor* é **sql_variant**, com um padrão de NULL. O tamanho de *value* não pode ser maior que 7.500 bytes.  
  
 [ @level0type =] {'*level0_object_type*'}  
 É o tipo de objeto de nível 0. *level0_object_type* é **varchar (128)**, com um padrão de NULL.  
  
 As entradas válidas são ASSEMBLY, CONTRACT, EVENT NOTIFICATION, FILEGROUP, MESSAGE TYPE, PARTITION FUNCTION, PARTITION SCHEME, REMOTE SERVICE BINDING, ROUTE, SCHEMA, SERVICE, USER, TRIGGER, TYPE, PLAN GUIDE e NULL.  
  
> [!IMPORTANT]  
>  A capacidade de especificar USER como um tipo de nível 0 em uma propriedade estendida de um objeto de tipo de nível 1 será removida em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Em vez disso, use SCHEMA como o tipo nível 0. Por exemplo, ao definir uma propriedade estendida em uma tabela, especifique o esquema da tabela em vez de um nome de usuário. A capacidade de especificar TYPE como um tipo de nível 0 será removida em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para TYPE, use SCHEMA como o tipo de nível 0 e TYPE como o tipo de nível 1.  
  
 [ @level0name =] {'*level0_object_name*'}  
 É o nome do tipo de objeto de nível 0 especificado. *level0_object_name* é **sysname** com um padrão de NULL.  
  
 [ @level1type =] {'*level1_object_type*'}  
 É o tipo de objeto de nível 1. *level1_object_type* é **varchar (128)**, com um padrão de NULL. As entradas válidas são AGREGAção, padrão, função, nome de arquivo lógico, procedimento, fila, regra, sequência, sinônimo, tabela, TABLE_TYPE, tipo, exibição, coleção de esquemas XML e nulo.    
 [ @level1name =] {'*level1_object_name*'}  
 É o nome do tipo de objeto de nível 1 especificado. *level1_object_name* é **sysname**, com um padrão de NULL.  
  
 [ @level2type =] {'*level2_object_type*'}  
 É o tipo de objeto de nível 2. *level2_object_type* é **varchar (128)**, com um padrão de NULL. As entradas válidas são COLUMN, CONSTRAINT, EVENT NOTIFICATION, INDEX, PARAMETER, TRIGGER e NULL.  
  
 [ @level2name =] {'*level2_object_name*'}  
 É o nome do tipo de objeto de nível 2 especificado. *level2_object_name* é **sysname**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Para especificar as propriedades estendidas, os objetos em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são classificados em três níveis: 0, 1 e 2. O nível 0 é o nível mais alto e está definido como objetos que estão contidos no escopo do banco de dados. Os objetos de nível 1 estão contidos em um esquema ou escopo de usuário e os objetos de nível 2 estão contidos pelos objetos de nível 1. As propriedades estendidas podem ser definidas para os objetos em qualquer um desses níveis.  
  
 As referências a um objeto de um nível precisam ser qualificadas com os nomes dos objetos de nível superior que as possua ou contenha. Por exemplo, ao adicionar uma propriedade estendida à coluna de uma tabela (nível 2), é necessário também especificar o nome da tabela (nível 1) que contém a coluna e o esquema (nível 0) que contém a tabela.  
  
 Se todos os tipos e nomes de objeto forem nulos, a propriedade pertencerá ao próprio banco de dados atual.  
  
 Propriedades estendidas não são permitidas em objetos de sistema, objetos fora do escopo de um banco de dados definido pelo usuário ou objetos não listados em Argumentos como entradas válidas.  
  
 As propriedades estendidas não são permitidas em tabelas com otimização de memória.  
  
## <a name="replicating-extended-properties"></a>Replicando propriedades estendidas  
 As propriedades estendidas são replicadas apenas na sincronização inicial entre o Editor e o Assinante. Se você adicionar ou modificar uma propriedade estendida depois da sincronização inicial, a alteração não será replicada. Para obter mais informações sobre como replicar objetos de banco de [dados, consulte Publish Data and Database Objects](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
## <a name="schema-vs-user"></a>Esquema x  Usuário  
 Não recomendamos a especificação de USER como um tipo de nível 0 ao aplicar uma propriedade estendida a um objeto de banco de dados, pois poderá criar ambiguidade na resolução de nome. Por exemplo, imagine que o usuário Mary seja proprietário dois esquemas (Mary e MySchema) e esses dois esquemas contenham uma tabela chamada MyTable. Se Mary adicionar uma propriedade estendida à tabela MyTable e especificar **@level0type = N'USER '**, **@level0name = Mary**, não será claro para qual tabela a propriedade estendida será aplicada. Para manter compatibilidade com versões anteriores, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplicará a propriedade à tabela contida no esquema chamado Mary.  
  
## <a name="permissions"></a>Permissões  
 Os membros das funções de banco de dados fixa db_owner e db_ddladmin podem adicionar propriedades estendidas a qualquer objeto com a seguinte exceção: db_ddladmin não pode adicionar propriedades ao banco de dados em si ou a usuários ou funções.  
  
 Os usuários podem adicionar propriedades estendidas a objetos que possuam ou para os quais tenham permissões ALTER ou CONTROL.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-adding-an-extended-property-to-a-database"></a>a. Adicionando uma propriedade estendida a um banco de dados  
 O exemplo a seguir adiciona o nome da propriedade `'Caption'` com um valor de `'AdventureWorks2012 Sample OLTP Database'` ao banco de dados de exemplo `AdventureWorks2012` .  
  
```  
USE AdventureWorks2012;  
GO  
--Add a caption to the AdventureWorks2012 Database object itself.  
EXEC sp_addextendedproperty   
@name = N'Caption',   
@value = 'AdventureWorks2012 Sample OLTP Database';  
```  
  
### <a name="b-adding-an-extended-property-to-a-column-in-a-table"></a>B. Adicionando uma propriedade estendida a uma coluna em uma tabela  
 O exemplo a seguir adiciona uma propriedade de legenda à coluna `PostalCode` na tabela `Address`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_addextendedproperty   
@name = N'Caption',   
@value = 'Postal code is a required column.',  
@level0type = N'Schema', @level0name = 'Person',  
@level1type = N'Table',  @level1name = 'Address',  
@level2type = N'Column', @level2name = 'PostalCode';  
GO  
```  
  
### <a name="c-adding-an-input-mask-property-to-a-column"></a>C. Adicionando uma propriedade de máscara de entrada a uma coluna  
 O exemplo a seguir adiciona uma propriedade de máscara de entrada '`99999 or 99999-9999 or #### ###`' à coluna `PostalCode` na tabela `Address`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_addextendedproperty   
@name = N'Input Mask ', @value = '99999 or 99999-9999 or #### ###',  
@level0type = N'Schema', @level0name = 'Person',  
@level1type = N'Table', @level1name = 'Address',   
@level2type = N'Column',@level2name = 'PostalCode';  
GO  
```  
  
### <a name="d-adding-an-extended-property-to-a-filegroup"></a>D. Adicionando uma propriedade estendida a um grupo de arquivos  
 O exemplo a seguir adiciona uma propriedade estendida ao grupo de arquivos `PRIMARY` .  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_DescriptionExample',   
@value = N'Primary filegroup for the AdventureWorks2012 sample database.',   
@level0type = N'FILEGROUP', @level0name = 'PRIMARY';  
GO  
```  
  
### <a name="e-adding-an-extended-property-to-a-schema"></a>E. Adicionando uma propriedade estendida a um esquema  
 O exemplo a seguir adiciona uma propriedade estendida ao esquema `HumanResources` .  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_addextendedproperty   
@name = N'MS_DescriptionExample',  
@value = N'Contains objects related to employees and departments.',  
@level0type = N'SCHEMA',   
@level0name = 'HumanResources';  
```  
  
### <a name="f-adding-an-extended-property-to-a-table"></a>F. Adicionando uma propriedade estendida a uma tabela  
 O exemplo a seguir adiciona uma propriedade estendida à tabela `Address` no esquema `Person` .  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_DescriptionExample',   
@value = N'Street address information for customers, employees, and vendors.',   
@level0type = N'SCHEMA', @level0name = 'Person',  
@level1type = N'TABLE',  @level1name = 'Address';  
GO  
```  
  
### <a name="g-adding-an-extended-property-to-a-role"></a>G. Adicionando uma propriedade estendida a uma função  
 O exemplo a seguir cria uma função de aplicativo e adiciona uma propriedade estendida à função.  
  
```  
USE AdventureWorks2012;   
GO  
CREATE APPLICATION ROLE Buyers  
WITH Password = '987G^bv876sPY)Y5m23';   
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_Description',   
@value = N'Application Role for the Purchasing Department.',  
@level0type = N'USER',  
@level0name = 'Buyers';  
```  
  
### <a name="h-adding-an-extended-property-to-a-type"></a>H. Adicionando uma propriedade estendida a um tipo  
 O exemplo a seguir adiciona uma propriedade estendida a um tipo.  
  
```  
USE AdventureWorks2012;   
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_Description',   
@value = N'Data type (alias) to use for any column that represents an order number. For example a sales order number or purchase order number.',   
@level0type = N'SCHEMA',   
@level0name = N'dbo',   
@level1type = N'TYPE',   
@level1name = N'OrderNumber';  
```  
  
### <a name="i-adding-an-extended-property-to-a-user"></a>I. Adicionando uma propriedade estendida a um usuário  
 O exemplo a seguir cria um usuário e adiciona uma propriedade estendida ao usuário.  
  
```  
USE AdventureWorks2012;   
GO  
CREATE USER CustomApp WITHOUT LOGIN ;   
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_Description',   
@value = N'User for an application.',   
@level0type = N'USER',   
@level0name = N'CustomApp';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.fn_listextendedproperty ](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropextendedproperty ](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [sp_updateextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updateextendedproperty-transact-sql.md)  
  
  
