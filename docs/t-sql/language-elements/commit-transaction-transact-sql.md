---
title: "CONFIRMAÇÃO de transação (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 09/09/2016
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COMMIT
- COMMIT TRANSACTION
- COMMIT_TSQL
- COMMIT_TRANSACTION_TSQL
dev_langs: TSQL
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
caps.latest.revision: "53"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 815d114944cfa233777fce1ba01c4639cc7417b3
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="commit-transaction-transact-sql"></a>COMMIT TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Marca o término de uma transação implícita ou explícita bem-sucedida. Se @@TRANCOUNT é 1, COMMIT TRANSACTION torna todas as modificações de dados efetuadas desde o início da transação uma parte permanente do banco de dados, libera os recursos mantidos pela transação e diminui @@TRANCOUNT como 0. Se @@TRANCOUNT é maior que 1, COMMIT TRANSACTION reduz @@TRANCOUNT somente por 1 e a transação permanece ativa.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 **Aplica-se a:** do SQL Server e banco de dados SQL do Azure
 
 É ignorado pelo [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. *transaction_name* Especifica um nome de transação atribuído por um BEGIN TRANSACTION anterior. *transaction_name*devem estar em conformidade com as regras para identificadores, mas não pode exceder 32 caracteres. *transaction_name* pode ser usado como um auxílio à legibilidade, indicando aos programadores a qual aninhada BEGIN TRANSACTION, COMMIT TRANSACTION está associado.  
  
 *@tran_name_variable*  
 **Aplica-se a:** do SQL Server e banco de dados SQL do Azure  
 
É o nome de uma variável definida pelo usuário que contém um nome de transação válido. A variável deve ser declarada com um tipo de dados char, varchar, nchar ou nvarchar. Se mais de 32 caracteres forem transmitidos à variável, apenas 32 caracteres serão usados; os demais serão truncados.  
  
 DELAYED_DURABILITY  
 **Aplica-se a:** do SQL Server e banco de dados SQL do Azure   

 Opção que solicita que esta transação seja confirmada com durabilidade atrasada. A solicitação será ignorada se o banco de dados for alterado com `DELAYED_DURABILITY = DISABLED` ou `DELAYED_DURABILITY = FORCED`. Consulte o tópico [controlar a durabilidade da transação](../../relational-databases/logs/control-transaction-durability.md) para obter mais informações.  
  
## <a name="remarks"></a>Remarks  
 É responsabilidade do programador do [!INCLUDE[tsql](../../includes/tsql-md.md)] emitir COMMIT TRANSACTION apenas no ponto em que todos os dados referidos pela transação estejam logicamente corretos.  
  
 Se a transação confirmada for uma transação distribuída de [!INCLUDE[tsql](../../includes/tsql-md.md)], COMMIT TRANSACTION irá disparar MS DTC para usar um protocolo 2PC para confirmar todos os servidores envolvidos na transação. Se uma transação local atingir dois ou mais bancos de dados na mesma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], essa instância usará um protocolo 2PC interno para confirmar todos os bancos de dados envolvidos na transação.  
  
 Quando usadas em transações aninhadas, as confirmações das transações internas não liberam recursos, nem lhes fazem modificações permanentes. As modificações de dados se tornam permanentes, com liberação dos recursos, apenas quando a transação externa é confirmada. Cada COMMIT TRANSACTION emitida quando @@TRANCOUNT é maior que 1 diminui simplesmente @@TRANCOUNT em 1. Quando @@TRANCOUNT é, finalmente, decrementado para 0, toda a transação externa for confirmada. Porque *transaction_name* é ignorado pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)], emitir uma COMMIT TRANSACTION referenciando o nome de uma transação externa quando há transações internas pendentes apenas decrementa @@TRANCOUNT em 1.  
  
 Emitir uma COMMIT TRANSACTION quando @@TRANCOUNT é 0 resulta em erro; não há BEGIN TRANSACTION correspondente.  
  
 Não é possível reverter uma transação após a emissão de uma instrução COMMIT TRANSACTION, porque as modificações de dados se tornam parte permanente do banco de dados.  
  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] incrementa a contagem de transações em uma instrução apenas quando essa contagem é 0 no início da instrução.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-committing-a-transaction"></a>A. Confirmar uma transação  
**Aplica-se a:** do SQL Server, banco de dados SQL do Azure, Azure SQL Data Warehouse e Parallel Data Warehouse   

O exemplo a seguir exclui um candidato a emprego. Ele usa o AdventureWorks. 
  
```   
BEGIN TRANSACTION;   
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;   
COMMIT TRANSACTION;   
```  
  
### <a name="b-committing-a-nested-transaction"></a>B. Confirmando uma transação aninhada  
**Aplica-se a:** do SQL Server e banco de dados SQL do Azure    

O exemplo a seguir cria uma tabela, gera três níveis de transações aninhadas e, em seguida, confirma a transação aninhada. Embora cada `COMMIT TRANSACTION` instrução possui um *transaction_name* parâmetro, não há nenhuma relação entre o `COMMIT TRANSACTION` e `BEGIN TRANSACTION` instruções. O *transaction_name* parâmetros são simplesmente à legibilidade, para ajudar o programador certifique-se de que o número adequado de confirmações esteja codificado para decrementar `@@TRANCOUNT` como 0 e, assim, confirmar a transação externa. 
  
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
  
## <a name="see-also"></a>Consulte também  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
