---
title: sp_bindrule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_bindrule_TSQL
- sp_bindrule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindrule
ms.assetid: 2606073e-c52f-498d-a923-5026b9d97e67
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 15576737e238ebd81d36e1ab2ff3090f6aa30791
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39560716"
---
# <a name="spbindrule-transact-sql"></a>sp_bindrule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Associa uma regra a uma coluna ou a um tipo de dados de alias.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use[Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md) em vez disso. Restrições CHECK são criadas usando a palavra-chave CHECK do [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) ou [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) instruções.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_bindrule [ @rulename = ] 'rule' ,   
     [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@rulename=**] **'***regra***'**  
 É o nome de uma regra criada pela instrução CREATE RULE. *regra* está **nvarchar(776)**, sem padrão.  
  
 [  **@objname=**] **'***object_name***'**  
 É a tabela e a coluna ou o tipo de dados de alias aos quais a regra será associada. Uma regra não pode ser associada a um **text**, **ntext**, **image**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **xml**, tipo de dado CLR definido pelo usuário ou uma coluna **timestamp**. A regra não pode ser associada a uma coluna computada.  
  
 *object_name* está **nvarchar(776)** sem nenhum padrão. Se *object_name* é um nome de uma parte, ele será resolvido como um tipo de dados de alias. Se for um nome composto de duas ou três partes, primeiro será resolvido como uma tabela e coluna e, se essa resolução falhar, será resolvido como um tipo de dados de alias. Por padrão, as colunas existentes do tipo de dados de alias herdam *regra* , a menos que uma regra foi associada diretamente à coluna.  
  
> [!NOTE]  
>  *object_name* pode conter o colchete **[** e **]** caracteres como caracteres de identificador delimitado. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
> [!NOTE]  
>  As regras criadas em expressões que usam tipos de dados de alias podem ser associadas colunas ou a tipos de dados de alias, mas falham ao compilar quando são referenciadas. Evite usar regras criadas em tipos de dados de alias.  
  
 [  **@futureonly=** ] **'***futureonly_flag***'**  
 É usado apenas ao associar uma regra a um tipo de dados de alias. *future_only_flag* está **varchar(15)** com um padrão NULL. Esse parâmetro quando definido como **futureonly** impede que as colunas existentes de um tipo de dados de alias herdem a nova regra. Se *futureonly_flag* for NULL, a nova regra é associada a quaisquer colunas do tipo de dados de alias que atualmente não tenham regra ou que estejam usando a regra existente do tipo de dados de alias.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 Você pode associar uma nova regra a uma coluna (embora o uso de uma restrição de verificação é preferível) ou a um tipo de dados de alias com **sp_bindrule** sem desassociar uma regra existente. A regra antiga é substituída. Se uma regra for associada a uma coluna com uma restrição CHECK existente, todas as restrições serão avaliadas. Não é possível associar uma regra a um tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A regra é imposta quando uma instrução INSERT é usada, mas não na associação. Você pode associar uma regra de caracteres para uma coluna de **numéricos** de tipo de dados, embora essa operação INSERT não é válida.  
  
 As colunas existentes do tipo de dados de alias herdam a nova regra, a menos que *futureonly_flag* é especificado como **futureonly**. As novas colunas definidas com o tipo de dados de alias sempre herdam a regra. Entretanto, se a cláusula ALTER COLUMN de uma instrução ALTER TABLE alterar o tipo de dados de uma coluna para um tipo de dados de alias associado a uma regra, a regra associada ao tipo de dados não será herdada pela coluna. A regra deve ser associada especificamente à coluna usando **sp_bindrule**.  
  
 Quando você associa uma regra a uma coluna, as informações relacionadas são adicionadas para o **sys. Columns** tabela. Quando você associa uma regra a um tipo de dados de alias, as informações relacionadas são adicionadas para o **Types** tabela.  
  
## <a name="permissions"></a>Permissões  
 Para associar uma regra a uma coluna de tabela, você deve ter a permissão ALTER na tabela. É necessário ter a permissão CONTROL no tipo de dados de alias ou a permissão ALTER no esquema ao qual o tipo pertence para associar uma regra a um tipo de dados de alias.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-binding-a-rule-to-a-column"></a>A. Associando uma regra a uma coluna  
 Supondo que uma regra chamada `today` tenha sido criada no banco de dados atual usando a instrução CREATE RULE, o exemplo a seguir associa a regra à coluna `HireDate` da tabela `Employee`. Quando uma linha é acrescentada a `Employee`, os dados para a coluna `HireDate` são verificados em relação à regra `today`.  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-rule-to-an-alias-data-type"></a>B. Associando uma regra a um tipo de dados de alias  
 Supondo a existência de uma regra chamada `rule_ssn` e um tipo de dados de alias chamado `ssn`, o exemplo a seguir associa `rule_ssn` a `ssn`. Em uma instrução CREATE TABLE, as colunas de tipo `ssn` herdam a regra `rule_ssn`. As colunas existentes do tipo `ssn` também herdam a `rule_ssn` de regra, a menos que **futureonly** é especificado para *futureonly_flag*, ou `ssn` tem uma regra associada diretamente a ele. As regras associadas a colunas sempre têm precedência sobre as associadas aos tipos de dados.  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'rule_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonlyflag"></a>C. Usando o futureonly_flag  
 O exemplo a seguir associa a regra `rule_ssn` ao tipo de dados de alias `ssn`. Como `futureonly` foi especificado, nenhuma coluna existente do tipo `ssn` será afetada.  
  
```  
USE master;  
GO  
EXEC sp_bindrule rule_ssn, 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. Usando identificadores delimitados  
 O exemplo a seguir mostra o uso de identificadores delimitados *object_name* parâmetro.  
  
```  
USE master;  
GO  
CREATE TABLE [t.2] (c1 int) ;  
-- Notice the period as part of the table name.  
EXEC sp_bindrule rule1, '[t.2].c1' ;  
-- The object contains two periods;   
-- the first is part of the table name   
-- and the second distinguishes the table name from the column name.  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [sp_unbindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
