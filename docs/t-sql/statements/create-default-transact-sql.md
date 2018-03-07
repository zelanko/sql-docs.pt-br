---
title: "Criar padrão (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 11/25/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a51a1045532b9194586d197c6b1b537d795d1996
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="create-default-transact-sql"></a>CREATE DEFAULT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cria um objeto chamado padrão. Quando associado a uma coluna ou um tipo de dados de alias, um padrão especifica um valor a ser inserido na coluna á qual o objeto está associado (ou em todas as colunas, no caso de um tipo de dados de alias), quando nenhum valor é fornecido explicitamente durante uma inserção.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez dela, use definições padrão criadas usando a palavra-chave DEFAULT de ALTER TABLE ou CREATE TABLE.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE DEFAULT [ schema_name . ] default_name   
AS constant_expression [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 É o nome do esquema ao qual o padrão pertence.  
  
 *default_name*  
 É o nome do padrão. Os nomes padrão devem obedecer às regras de [identificadores](../../relational-databases/databases/database-identifiers.md). Especificar o nome do proprietário do padrão é opcional.  
  
 *constant_expression*  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) que contém somente valores constantes (não pode incluir os nomes de todas as colunas ou outros objetos de banco de dados). Podem ser usadas qualquer constante, função interna ou expressão matemática, menos aquelas que contêm tipos de dados de alias. Funções definidas pelo usuário não podem ser usadas. Coloque constantes de caractere e data entre aspas simples (**'**); monetárias, inteiro e constantes de ponto flutuante não requerem aspas. Dados binários devem ser precedidos por 0x e dados monetários por um sinal de dólar ($). O valor padrão deve ser compatível com o tipo de dados de coluna.  
  
## <a name="remarks"></a>Remarks  
 Um nome padrão pode ser criado somente no banco de dados atual. Dentro de um banco de dados, os nomes padrão devem ser exclusivos por esquema. Quando um padrão é criado, use **sp_bindefault** para associá-lo a uma coluna ou a um tipo de dados de alias.  
  
 Se o padrão não for compatível com a coluna à qual está associado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará uma mensagem de erro ao tentar inserir o valor padrão. Por exemplo, n/d não pode ser usado como um padrão para um **numérico** coluna.  
  
 Se o valor padrão for muito longo para a coluna à qual está associado, ele será truncado.  
  
 Instruções CREATE DEFAULT não podem ser combinadas com outras instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] em um único lote.  
  
 Um padrão deve ser descartado antes de criar um novo de mesmo nome e o padrão deve ser desassociado executando **sp_unbindefault** antes de ser descartado.  
  
 Se uma coluna tiver um padrão e uma regra associado a ele, o valor do padrão não deve violar a regra. Um padrão que entra em conflito com uma regra nunca é inserido, e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera uma mensagem de erro sempre que tenta inseri-lo.  
  
 Ao ser associado a uma coluna, um valor padrão é inserido quando:  
  
-   Um valor não é inserido explicitamente.  
  
-   As palavras-DEFAULT VALUES ou DEFAULT são usadas com INSERT para inserir valores padrão.  
  
 Se NOT NULL for especificado ao criar uma coluna e um padrão não for criado para ela, uma mensagem de erro será gerada quando um usuário não fizer uma entrada nessa coluna. A tabela a seguir ilustra o relacionamento entre a existência de um padrão e a definição de uma coluna como NULL ou NOT NULL. As entradas na tabela mostram o resultado.  
  
|Definição da coluna|Nenhuma entrada, nenhum padrão|Nenhuma entrada, padrão|Insere NULL, nenhum padrão|Insere NULL, padrão|  
|-----------------------|--------------------------|-----------------------|----------------------------|-------------------------|  
|**NULL**|NULL|padrão|NULL|NULL|  
|**NOT NULL**|Erro|padrão|erro|erro|  
  
 Para renomear um padrão, use **sp_rename**. Para um relatório em um padrão, use **sp_help**.  
  
## <a name="permissions"></a>Permissões  
 Para executar CREATE DEFAULT, no mínimo, um usuário deve ter a permissão CREATE DEFAULT no banco de dados atual e a permissão ALTER no esquema no qual o padrão está sendo criado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-simple-character-default"></a>A. Criando um padrão de caractere simples  
 O exemplo a seguir cria um padrão de caractere chamado `unknown`.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE DEFAULT phonedflt AS 'unknown';  
```  
  
### <a name="b-binding-a-default"></a>B. Associando um padrão  
 O exemplo a seguir associa o padrão criado no exemplo A. O padrão entra em vigor somente se nenhuma entrada for especificada para a coluna `Phone` da tabela `Contact`. Observe que omitir qualquer entrada é diferente de declarar NULL explicitamente em uma instrução INSERT.  
  
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
 [Remover padrão &#40; Transact-SQL &#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [Remover regra &#40; Transact-SQL &#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [Expressões &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [sp_bindefault &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindefault &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)  
  
  
