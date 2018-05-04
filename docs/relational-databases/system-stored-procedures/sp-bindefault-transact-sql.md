---
title: sp_bindefault (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_bindefault
- sp_bindefault_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindefault
ms.assetid: 3da70c10-68d0-4c16-94a5-9e84c4a520f6
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 67d46825f0da450707710c600cacb549d370082c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spbindefault-transact-sql"></a>sp_bindefault (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Associa um padrão a uma coluna ou a um tipo de dados de alias.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] É recomendável criar definições padrão usando a palavra-chave DEFAULT do [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) instruções em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_bindefault [ @defname = ] 'default' ,   
    [ @objname = ] 'object_name'   
    [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@defname=** ] **'***padrão***'**  
 É o nome do valor padrão criado por CREATE DEFAULT. *padrão* é **nvarchar(776)**, sem padrão.  
  
 [  **@objname=** ] **'***object_name***'**  
 É o nome da tabela e da coluna ou o tipo de dados de alias aos quais o valor padrão será associado. *object_name* é **nvarchar(776)** sem nenhum padrão. *object_name* não pode ser definido com o **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, ou CLR tipos definidos pelo usuário.  
  
 Se *object_name* é um nome de uma parte, ele será resolvido como um tipo de dados de alias. Se for um nome de duas ou três partes, primeiro será resolvido como uma tabela e coluna; e se essa resolução falhar, ele será resolvido como um tipo de dados de alias. Por padrão, as colunas existentes do tipo de dados de alias herdam *padrão*, a menos que um padrão foi associado diretamente à coluna. Um padrão não pode ser associado a um **texto**, **ntext**, **imagem**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, **timestamp**, ou CLR coluna de tipo definido pelo usuário, uma coluna com a propriedade IDENTITY, uma coluna computada ou uma coluna que já tem uma restrição padrão.  
  
> [!NOTE]  
>  *object_name* pode conter colchetes **[]** como identificadores delimitados. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
 [  **@futureonly=** ] **'***futureonly_flag***'**  
 É usado apenas ao associar um padrão a um tipo de dados de alias. *futureonly_flag* é **varchar(15)** com um padrão NULL. Quando esse parâmetro é definido como **futureonly**, as colunas existentes desse tipo de dados não podem herdar o novo padrão. Este parâmetro nunca é usado ao associar um padrão a uma coluna. Se *futureonly_flag* for NULL, o novo padrão é associado a quaisquer colunas do tipo de dados de alias que atualmente não tenham padrão ou que estejam usando o padrão existente do tipo de dados de alias.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 Você pode usar **sp_bindefault** para vincular um novo padrão a uma coluna, embora o uso da restrição DEFAULT seja preferido, ou a um tipo de dados de alias sem desvinculando um padrão existente. O padrão antigo será substituído. Você não pode associar um padrão a um tipo de dados de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou a um tipo de dado CLR definido pelo usuário. Se o padrão não for compatível com a coluna à qual ele foi associado, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] retornará uma mensagem de erro ao tentar inserir o valor padrão, não ao associá-lo.  
  
 As colunas existentes do tipo de dados de alias herdam o novo padrão, a menos que um padrão é associado diretamente a eles ou *futureonly_flag* é especificado como **futureonly**. As novas colunas do tipo de dados de alias sempre herdam o padrão.  
  
 Quando você associa um padrão a uma coluna, as informações relacionadas são adicionadas para o **Columns** exibição do catálogo. Quando você associa um padrão para um tipo de dados de alias, as informações relacionadas são adicionadas para o **Types** exibição do catálogo.  
  
## <a name="permissions"></a>Permissões  
 Usuário deve possuir a tabela ou ser um membro do **sysadmin** função fixa de servidor ou o **db_owner** e **db_ddladmin** funções de banco de dados fixas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-binding-a-default-to-a-column"></a>A. Associando um padrão a uma coluna  
 Um padrão denominado `today` foi definido no banco de dados atual usando CREATE DEFAULT; o exemplo a seguir associa o padrão à coluna `HireDate` da tabela `Employee`. Sempre que uma linha for adicionada à tabela `Employee` e os dados da coluna `HireDate` não forem fornecidos, a coluna obterá o valor do padrão `today`.  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-default-to-an-alias-data-type"></a>B. Associando um padrão a um tipo de dados de alias.  
 Já existem um padrão denominado `def_ssn` e um tipo de dados de alias denominado `ssn`. O exemplo a seguir associa o padrão `def_ssn` a `ssn`. Quando uma tabela for criada, o padrão será herdado por todas as colunas que tenham o tipo de dados de alias `ssn` designado. As colunas existentes do tipo **ssn** também herdam o padrão **def_ssn**, a menos que **futureonly** é especificado para *futureonly_flag* valor ou, a menos que a coluna tem um padrão associado diretamente a ela. Os padrões associados a colunas sempre têm precedência aos associados a tipos de dados.  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonlyflag"></a>C. Usando o futureonly_flag  
 O exemplo a seguir associa o padrão `def_ssn` ao tipo de dados de alias `ssn`. Porque **futureonly** for especificado, nenhuma coluna existente do tipo `ssn` são afetados.  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. Usando identificadores delimitados  
 O exemplo a seguir mostra o uso de identificadores delimitados, `[t.1]`, na *object_name*.  
  
```  
USE master;  
GO  
CREATE TABLE [t.1] (c1 int);   
-- Notice the period as part of the table name.  
EXEC sp_bindefault 'default1', '[t.1].c1' ;  
-- The object contains two periods;   
-- the first is part of the table name,   
-- and the second distinguishes the table name from the column name.  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [sp_unbindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
