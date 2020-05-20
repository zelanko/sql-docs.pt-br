---
title: sp_bindefault (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_bindefault
- sp_bindefault_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindefault
ms.assetid: 3da70c10-68d0-4c16-94a5-9e84c4a520f6
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b1552f566852f90b3526645313a160f2446b868e
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828471"
---
# <a name="sp_bindefault-transact-sql"></a>sp_bindefault (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Associa um padrão a uma coluna ou a um tipo de dados de alias.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Recomendamos que você crie definições padrão usando a palavra-chave DEFAULT das instruções [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_bindefault [ @defname = ] 'default' ,   
    [ @objname = ] 'object_name'   
    [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @defname = ] 'default'`É o nome do padrão que é criado por criar padrão. o *padrão* é **nvarchar (776)**, sem padrão.  
  
`[ @objname = ] 'object_name'`É o nome da tabela e da coluna ou do tipo de dados do alias ao qual o padrão deve ser associado. *object_name* é **nvarchar (776)** sem padrão. Não é possível definir *object_name* com os tipos **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **XML**ou CLR definidos pelo usuário.  
  
 Se *object_name* for um nome de uma parte, ele será resolvido como um tipo de dados de alias. Se for um nome de duas ou três partes, ele será resolvido primeiro como uma tabela e uma coluna; e se essa resolução falhar, ela será resolvida como um tipo de dados de alias. Por padrão, as colunas existentes do tipo de dados alias herdam *Default*, a menos que um padrão tenha sido associado diretamente à coluna. Um padrão não pode ser associado a uma coluna de tipo **Text**, **ntext**, **Image**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **XML**, **timestamp**ou CLR definida pelo usuário, uma coluna com a propriedade Identity, uma coluna computada ou uma coluna que já tenha uma restrição default.  
  
> [!NOTE]  
>  *object_name* pode conter colchetes **[]** como identificadores delimitados. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
`[ @futureonly = ] 'futureonly_flag'`É usado somente ao associar um padrão a um tipo de dados de alias. *futureonly_flag* é **varchar (15)** com um padrão de NULL. Quando esse parâmetro é definido como **futureonly**, as colunas existentes desse tipo de dados não podem herdar o novo padrão. Este parâmetro nunca é usado ao associar um padrão a uma coluna. Se *futureonly_flag* for NULL, o novo padrão será associado a qualquer coluna do tipo de dados de alias que atualmente não tem nenhum padrão ou que esteja usando o padrão existente do tipo de dados de alias.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Você pode usar **sp_bindefault** para associar um novo padrão a uma coluna, embora o uso da restrição padrão seja preferencial ou a um tipo de dados de alias sem a desvinculação de um padrão existente. O padrão antigo será substituído. Você não pode associar um padrão a um tipo de dados de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou a um tipo de dado CLR definido pelo usuário. Se o padrão não for compatível com a coluna à qual ele foi associado, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] retornará uma mensagem de erro ao tentar inserir o valor padrão, não ao associá-lo.  
  
 As colunas existentes do tipo de dados alias herdam o novo padrão, a menos que um padrão esteja associado diretamente a eles ou *futureonly_flag* seja especificado como **futureonly**. As novas colunas do tipo de dados de alias sempre herdam o padrão.  
  
 Quando você associa um padrão a uma coluna, as informações relacionadas são adicionadas à exibição do catálogo **Sys. Columns** . Quando você associa um padrão a um tipo de dados de alias, informações relacionadas são adicionadas à exibição de catálogo **Sys. Types** .  
  
## <a name="permissions"></a>Permissões  
 O usuário deve possuir a tabela ou ser um membro da função de servidor fixa **sysadmin** ou o **db_owner** e **db_ddladmin** funções de banco de dados fixas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-binding-a-default-to-a-column"></a>a. Associando um padrão a uma coluna  
 Um padrão denominado `today` foi definido no banco de dados atual usando CREATE DEFAULT; o exemplo a seguir associa o padrão à coluna `HireDate` da tabela `Employee`. Sempre que uma linha for adicionada à tabela `Employee` e os dados da coluna `HireDate` não forem fornecidos, a coluna obterá o valor do padrão `today`.  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-default-to-an-alias-data-type"></a>B. Associando um padrão a um tipo de dados de alias.  
 Já existem um padrão denominado `def_ssn` e um tipo de dados de alias denominado `ssn`. O exemplo a seguir associa o padrão `def_ssn` a `ssn`. Quando uma tabela for criada, o padrão será herdado por todas as colunas que tenham o tipo de dados de alias `ssn` designado. As colunas existentes do tipo **ssn** também herdam o **def_ssn**padrão, a menos que **futureonly** seja especificado para *futureonly_flag* valor, ou a menos que a coluna tenha um padrão associado diretamente a ela. Os padrões associados a colunas sempre têm precedência aos associados a tipos de dados.  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonly_flag"></a>C. Usando o futureonly_flag  
 O exemplo a seguir associa o padrão `def_ssn` ao tipo de dados de alias `ssn`. Como **futureonly** é especificado, nenhuma coluna existente do tipo `ssn` é afetada.  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. Usando identificadores delimitados  
 O exemplo a seguir mostra o uso de identificadores delimitados, `[t.1]` , em *object_name*.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [Descartar padrão &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_unbindefault](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
