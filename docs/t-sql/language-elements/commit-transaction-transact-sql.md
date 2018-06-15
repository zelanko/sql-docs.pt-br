---
title: COMMIT TRANSACTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COMMIT
- COMMIT TRANSACTION
- COMMIT_TSQL
- COMMIT_TRANSACTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ending transactions [SQL Server]
- user-defined transactions [SQL Server]
- committed transactions
- transactions [SQL Server], ending
- marking end of transactions [SQL Server]
- implicit transactions
- distributed transactions [SQL Server], committed
- transactions [SQL Server], committed
- COMMIT TRANSACTION statement
- rolling back transactions, COMMIT TRANSACTION
ms.assetid: f8fe26a9-7911-497e-b348-4e69c7435dc1
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 95cf2d72d7e522d672ad791388a317cae8467ca3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33063713"
---
# <a name="commit-transaction-transact-sql"></a>COMMIT TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Marca o término de uma transação implícita ou explícita bem-sucedida. Se @@TRANCOUNT for 1, COMMIT TRANSACTION fará com que todas as modificações de dados executadas desde o início da transação sejam uma parte permanente do banco de dados, liberará os recursos mantidos pela transação e decrementará @@TRANCOUNT para 0. Se @@TRANCOUNT for maior que 1, COMMIT TRANSACTION decrementará @@TRANCOUNT somente em 1 e a transação permanecerá ativa.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Applies to SQL Server (starting with 2008) and Azure SQL Database
  
COMMIT [ { TRAN | TRANSACTION }  [ transaction_name | @tran_name_variable ] ] [ WITH ( DELAYED_DURABILITY = { OFF | ON } ) ]  
[ ; ]  
```  
 
```  
-- Applies to Azure SQL Data Warehouse and Parallel Data Warehouse Database
  
COMMIT [ TRAN | TRANSACTION ] 
[ ; ]  
``` 
 
  
## <a name="arguments"></a>Argumentos  
 *transaction_name*  
 **APLICA-SE A:** SQL Server e Banco de Dados SQL do Azure
 
 É ignorado pelo [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. *transaction_name* especifica um nome de transação atribuído por um BEGIN TRANSACTION anterior. *transaction_name* precisa estar em conformidade com as regras para identificadores, mas não pode exceder 32 caracteres. *transaction_name* pode ser usado para facilitar a leitura, indicando aos programadores a qual BEGIN TRANSACTION aninhada o COMMIT TRANSACTION está associado.  
  
 *@tran_name_variable*  
 **APLICA-SE A:** SQL Server e Banco de Dados SQL do Azure  
 
É o nome de uma variável definida pelo usuário que contém um nome de transação válido. A variável precisa ser declarada com o tipo de dados char, varchar, nchar ou nvarchar. Se mais de 32 caracteres forem transmitidos à variável, apenas 32 caracteres serão usados; os demais serão truncados.  
  
 DELAYED_DURABILITY  
 **APLICA-SE A:** SQL Server e Banco de Dados SQL do Azure   

 Opção que solicita que esta transação seja confirmada com durabilidade atrasada. A solicitação será ignorada se o banco de dados for alterado com `DELAYED_DURABILITY = DISABLED` ou `DELAYED_DURABILITY = FORCED`. Confira o tópico [Controlar a durabilidade da transação](../../relational-databases/logs/control-transaction-durability.md) para obter mais informações.  
  
## <a name="remarks"></a>Remarks  
 É responsabilidade do programador do [!INCLUDE[tsql](../../includes/tsql-md.md)] emitir COMMIT TRANSACTION apenas no ponto em que todos os dados referidos pela transação estejam logicamente corretos.  
  
 Se a transação confirmada for uma transação distribuída de [!INCLUDE[tsql](../../includes/tsql-md.md)], COMMIT TRANSACTION irá disparar MS DTC para usar um protocolo 2PC para confirmar todos os servidores envolvidos na transação. Se uma transação local atingir dois ou mais bancos de dados na mesma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], essa instância usará um protocolo 2PC interno para confirmar todos os bancos de dados envolvidos na transação.  
  
 Quando usadas em transações aninhadas, as confirmações das transações internas não liberam recursos, nem lhes fazem modificações permanentes. As modificações de dados se tornam permanentes, com liberação dos recursos, apenas quando a transação externa é confirmada. Cada COMMIT TRANSACTION emitido quando @@TRANCOUNT é maior que 1 simplesmente decrementa @@TRANCOUNT em 1. Quando @@TRANCOUNT é, finalmente, decrementado para 0, toda a transação externa é confirmada. Como *transaction_name* é ignorado pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)], emitir um COMMIT TRANSACTION referenciando o nome de uma transação externa quando há transações internas pendentes apenas decrementa @@TRANCOUNT em 1.  
  
 Emitir um COMMIT TRANSACTION quando @@TRANCOUNT é 0 resulta em erro. Não há um BEGIN TRANSACTION correspondente.  
  
 Não é possível reverter uma transação após a emissão de uma instrução COMMIT TRANSACTION, porque as modificações de dados se tornam parte permanente do banco de dados.  
  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] incrementa a contagem de transações em uma instrução apenas quando essa contagem é 0 no início da instrução.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-committing-a-transaction"></a>A. Confirmando uma transação  
**Aplica-se a:** SQL Server, Banco de Dados SQL do Azure, SQL Data Warehouse do Azure e Parallel Data Warehouse   

O exemplo a seguir exclui um candidato a emprego. Ele usa o AdventureWorks. 
  
```   
BEGIN TRANSACTION;   
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;   
COMMIT TRANSACTION;   
```  
  
### <a name="b-committing-a-nested-transaction"></a>B. Confirmando uma transação aninhada  
**APLICA-SE A:** SQL Server e Banco de Dados SQL do Azure    

O exemplo a seguir cria uma tabela, gera três níveis de transações aninhadas e, em seguida, confirma a transação aninhada. Embora cada instrução `COMMIT TRANSACTION` tenha um parâmetro *transaction_name*, não há nenhuma relação entre as instruções `COMMIT TRANSACTION` e `BEGIN TRANSACTION`. Os parâmetros *transaction_name* são simplesmente auxílios para facilitar a leitura, ajudando o programador a assegurar que o número adequado de confirmações seja codificado para decrementar `@@TRANCOUNT` para 0 e, assim, confirmar a transação externa. 
  
```   
IF OBJECT_ID(N'TestTran',N'U') IS NOT NULL  
    DROP TABLE TestTran;  
GO  
CREATE TABLE TestTran (Cola int PRIMARY KEY, Colb char(3));  
GO  
-- This statement sets @@TRANCOUNT to 1.  
BEGIN TRANSACTION OuterTran;  
  
PRINT N'Transaction count after BEGIN OuterTran = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
 
INSERT INTO TestTran VALUES (1, 'aaa');  
 
-- This statement sets @@TRANCOUNT to 2.  
BEGIN TRANSACTION Inner1;  
 
PRINT N'Transaction count after BEGIN Inner1 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
INSERT INTO TestTran VALUES (2, 'bbb');  
  
-- This statement sets @@TRANCOUNT to 3.  
BEGIN TRANSACTION Inner2;  
  
PRINT N'Transaction count after BEGIN Inner2 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
INSERT INTO TestTran VALUES (3, 'ccc');  
  
-- This statement decrements @@TRANCOUNT to 2.  
-- Nothing is committed.  
COMMIT TRANSACTION Inner2;  
 
PRINT N'Transaction count after COMMIT Inner2 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
 
-- This statement decrements @@TRANCOUNT to 1.  
-- Nothing is committed.  
COMMIT TRANSACTION Inner1;  
 
PRINT N'Transaction count after COMMIT Inner1 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
-- This statement decrements @@TRANCOUNT to 0 and  
-- commits outer transaction OuterTran.  
COMMIT TRANSACTION OuterTran;  
  
PRINT N'Transaction count after COMMIT OuterTran = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
```  
  
## <a name="see-also"></a>Consulte Também  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
