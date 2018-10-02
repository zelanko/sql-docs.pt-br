---
title: XACT_STATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- XACT_STATE
- XACT_STATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- states [SQL Server], transactions
- uncommittable transactions
- sessions [SQL Server], active transactions
- XACT_STATE function
- transactions [SQL Server], state
- active transactions
ms.assetid: e9300827-e793-4eb6-9042-ffa0204aeb50
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d74e1ebfb3f1d8e2bc36c2a4bd0432a830934b5d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47799334"
---
# <a name="xactstate-transact-sql"></a>XACT_STATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  É uma função escalar que informa o estado de transação de usuário de uma solicitação em execução atualmente. XACT_STATE indica se a solicitação tem uma transação de usuário ativa e se a transação consegue ser confirmada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
XACT_STATE()  
```  
  
## <a name="return-type"></a>Tipo de retorno  
 **smallint**  
  
## <a name="remarks"></a>Remarks  
 XACT_STATE retorna um dos valores a seguir.  
  
|Valor retornado|Significado|  
|------------------|-------------|  
|1|A solicitação atual tem uma transação de usuário ativa. A solicitação pode executar qualquer ação, inclusive escrever dados e confirmar a transação.|  
|0|Não há transação de usuário ativa para a solicitação atual.|  
|-1|A solicitação atual tem uma transação de usuário ativa, mas ocorreu um erro que fez a transação ser classificada como não confirmável. A solicitação não pode confirmar a transação ou reverter para um ponto de salvamento; ela só pode solicitar uma reversão completa da transação. A solicitação não pode executar nenhuma operação de gravação reverter a transação. A solicitação só pode executar operações de leitura até reverter a transação. Depois que a transação é revertida, a solicitação pode executar operações de leitura e gravação e pode começar uma nova transação.<br /><br /> Quando um lote externo conclui a execução, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] reverte automaticamente todas as transações ativas não confirmáveis. Se nenhuma mensagem de erro foi enviada quando a transação entrou em um estado não confirmável, quando o lote terminar, uma mensagem de erro será enviada ao aplicativo cliente. Essa mensagem indica que uma transação não confirmável foi detectada e revertida.|  
  
 As funções XACT_STATE e @@TRANCOUNT podem ambas ser usadas para detectar se a solicitação atual tem uma transação de usuário ativa. @@TRANCOUNT não pode ser usado para determinar se essa transação foi classificada como uma transação não confirmável. XACT_STATE não pode ser usado para determinar se há transações aninhadas.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `XACT_STATE` no bloco `CATCH` de uma construção `TRY…CATCH` para determinar se uma transação será confirmada ou revertida. Como `SET XACT_ABORT` é `ON`, o erro de violação de restrição faz a transação entrar em um estado não confirmável.  
  
```  
USE AdventureWorks2012;  
GO  
  
-- SET XACT_ABORT ON will render the transaction uncommittable  
-- when the constraint violation occurs.  
SET XACT_ABORT ON;  
  
BEGIN TRY  
    BEGIN TRANSACTION;  
        -- A FOREIGN KEY constraint exists on this table. This   
        -- statement will generate a constraint violation error.  
        DELETE FROM Production.Product  
            WHERE ProductID = 980;  
  
    -- If the delete operation succeeds, commit the transaction. The CATCH  
    -- block will not execute.  
    COMMIT TRANSACTION;  
END TRY  
BEGIN CATCH  
    -- Test XACT_STATE for 0, 1, or -1.  
    -- If 1, the transaction is committable.  
    -- If -1, the transaction is uncommittable and should   
    --     be rolled back.  
    -- XACT_STATE = 0 means there is no transaction and  
    --     a commit or rollback operation would generate an error.  
  
    -- Test whether the transaction is uncommittable.  
    IF (XACT_STATE()) = -1  
    BEGIN  
        PRINT 'The transaction is in an uncommittable state.' +  
              ' Rolling back transaction.'  
        ROLLBACK TRANSACTION;  
    END;  
  
    -- Test whether the transaction is active and valid.  
    IF (XACT_STATE()) = 1  
    BEGIN  
        PRINT 'The transaction is committable.' +   
              ' Committing transaction.'  
        COMMIT TRANSACTION;     
    END;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  
