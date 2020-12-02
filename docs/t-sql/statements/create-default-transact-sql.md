---
description: CREATE DEFAULT (Transact-SQL)
title: CREATE DEFAULT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_DEFAULT_TSQL
- CREATE DEFAULT
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], default
- default objects
- CREATE DEFAULT statement
- objects [SQL Server], creating
- DEFAULT definition
ms.assetid: 08475db4-7d90-486a-814c-01a99d783d41
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 15f0d4281b194a63e8441cade19a5d519bf2b4c0
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128030"
---
# <a name="create-default-transact-sql"></a>CREATE DEFAULT (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Cria um objeto chamado padrão. Quando associado a uma coluna ou a um tipo de dados de alias, um padrão especifica um valor a ser inserido na coluna à qual o objeto está associado (ou em todas as colunas, no caso de um tipo de dados de alias), quando nenhum valor é fornecido explicitamente durante uma inserção.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez dela, use definições padrão criadas usando a palavra-chave DEFAULT de ALTER TABLE ou CREATE TABLE.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
CREATE DEFAULT [ schema_name . ] default_name   
AS constant_expression [ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*schema_name*  
 O nome do esquema ao qual o padrão pertence.  
  
*default_name*  
 O nome do padrão. Os nomes padrão devem estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md). Especificar o nome do proprietário do padrão é opcional.  
  
*constant_expression*  
Uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) que contém somente valores constantes (não pode incluir os nomes de nenhuma coluna ou outros objetos de banco de dados). Você pode usar qualquer constante, função interna ou expressão matemática, menos aquelas que contêm tipos de dados de alias. As funções definidas pelo usuário não podem ser usadas. Coloque as constantes de caractere e de data entre aspas simples (**'**); as constantes monetárias, de inteiro e de ponto flutuante não exigem aspas. Dados binários devem ser precedidos por 0x e dados monetários por um sinal de dólar ($). O valor padrão deve ser compatível com o tipo de dados de coluna.  
  
## <a name="remarks"></a>Comentários  
 Só é possível criar um nome padrão no banco de dados atual. Dentro de um banco de dados, os nomes padrão devem ser exclusivos por esquema. Quando você criar um padrão, use **sp_bindefault** para associá-lo a uma coluna ou a um tipo de dados de alias.  
  
 Se o padrão não for compatível com a coluna à qual está associado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará uma mensagem de erro ao tentar inserir o valor padrão. Por exemplo, N/D não pode ser usado como padrão para uma coluna **numeric**.  
  
 Se o valor padrão for muito longo para a coluna à qual está associado, ele será truncado.  
  
 As instruções CREATE DEFAULT não podem ser combinadas com outras instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] em um único lote.  
  
 Um padrão deve ser descartado para que um novo com o mesmo nome seja criado. E o padrão deve ser desassociado executando **sp_unbindefault** antes de ser descartado.  
  
 Se uma coluna tiver um padrão e uma regra associado a ele, o valor do padrão não deve violar a regra. Um padrão que entra em conflito com uma regra nunca é inserido, e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera uma mensagem de erro sempre que tenta inseri-lo.  
  
 Ao ser associado a uma coluna, um valor padrão é inserido quando:  
  
-   Um valor não é inserido explicitamente.  
  
-   As palavras-DEFAULT VALUES ou DEFAULT são usadas com INSERT para inserir valores padrão.  
  
 Se você especificar NOT NULL ao criar uma coluna e não criar um padrão para ela, uma mensagem de erro será gerada quando um usuário não fizer uma entrada nessa coluna. A tabela a seguir ilustra o relacionamento entre a existência de um padrão e a definição de uma coluna como NULL ou NOT NULL. As entradas na tabela mostram o resultado.  
  
|Definição da coluna|Nenhuma entrada, nenhum padrão|Nenhuma entrada, padrão|Insere NULL, nenhum padrão|Insere NULL, padrão|  
|-----------------------|--------------------------|-----------------------|----------------------------|-------------------------|  
|**NULL**|NULO|default|NULO|NULO|  
|**NOT NULL**|Erro|default|erro|error|  
  
 Para renomear um padrão, use **sp_rename**. Para obter um relatório sobre um padrão, use **sp_help**.  
  
## <a name="permissions"></a>Permissões  
 Para usar CREATE DEFAULT, no mínimo, um usuário deve ter a permissão CREATE DEFAULT no banco de dados atual e a permissão ALTER no esquema no qual o padrão está sendo criado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-simple-character-default"></a>a. Criando um padrão de caractere simples  
 O exemplo a seguir cria um padrão de caractere chamado `unknown`.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE DEFAULT phonedflt AS 'unknown';  
```  
  
### <a name="b-binding-a-default"></a>B. Associando um padrão  
 O exemplo a seguir associa o padrão criado no exemplo A. O padrão entra em vigor somente se nenhuma entrada for especificada para a coluna `Phone` da tabela `Contact`. 
 
 > [!Note] 
 >  Omitir qualquer entrada é diferente de declarar NULL explicitamente em uma instrução INSERT.  
  
 Como não existe um padrão chamado `phonedflt`, a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir gera uma falha. Este exemplo é apenas uma ilustração.  
  
```sql  
USE AdventureWorks2012;  
GO  
sp_bindefault 'phonedflt', 'Person.PersonPhone.PhoneNumber';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [sp_bindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)  
  
  
