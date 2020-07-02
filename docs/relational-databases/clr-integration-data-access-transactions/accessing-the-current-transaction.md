---
title: Acessando a transação atual | Microsoft Docs
description: No SQL Server integração CLR, a propriedade atual da classe System. Transactions. Transaction permite que você acesse a transação atual.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- current transaction access
- Current property
- Transaction class
ms.assetid: 1a4e2ce5-f627-4c81-8960-6a9968cefda2
author: rothja
ms.author: jroth
ms.openlocfilehash: c82c4e4f5b1f1af6194ff409a684ca239881487a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765404"
---
# <a name="accessing-the-current-transaction"></a>Acessando a transação atual
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Se uma transação estiver ativa no ponto em que o código CLR (Common Language Runtime) que está sendo executado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for inserido, ela será exposta pela classe **System.Transactions.Transaction** . A propriedade **Transaction.Current** é usada para acessar a transação atual. Na maioria das vezes, não é necessário acessar a transação explicitamente. Para conexões de banco de dados, ADO.NET verifica **Transaction.Current** automaticamente quando o método **Connection.Open** é chamado e inscreve a conexão de forma transparente nessa transação (a menos que a palavra-chave **Enlist** esteja definida como falsa na cadeia de conexão).  
  
 Convém usar o objeto **Transaction** diretamente nos seguintes cenários:  
  
-   Se você desejar inscrever um recurso que não faz inscrição automática ou que, por algum motivo, não foi inscrito durante a inicialização.  
  
-   Se você desejar inscrever um recurso explicitamente na transação.  
  
-   Se você quiser finalizar a transação externa de dentro do seu procedimento armazenado ou função. Nesse caso, use <xref:System.Transactions.TransactionScope>. Por exemplo, o código a seguir reverterá a transação atual:  
  
    ```  
    using(TransactionScope transactionScope = new TransactionScope(TransactionScopeOptions.Required)) { }  
    ```  
  
 O resto deste tópico descreve outras maneiras de cancelar uma transação externa.  
  
## <a name="canceling-an-external-transaction"></a>Cancelando uma transação externa  
 Você pode cancelar transações externas em uma função ou em um procedimento gerenciado das seguintes maneiras:  
  
-   A função ou o procedimento gerenciado pode retornar um valor usando um parâmetro de saída. O procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)] de chamada pode verificar o valor retornado e, se apropriado, executar **ROLLBACK TRANSACTION**.  
  
-   A função ou o procedimento gerenciado pode gerar uma exceção personalizada. O procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)] de chamada pode capturar a exceção gerada pela função ou pelo procedimento gerenciado em um bloco try/catch e executar **ROLLBACK TRANSACTION**.  
  
-   A função ou o procedimento gerenciado poderá cancelar a transação atual chamando o método **Transaction.Rollback** se uma determinada condição for atendida.  
  
 Quando é chamado dentro de uma função ou um procedimento gerenciado, o método **Transaction.Rollback** gera uma exceção com uma mensagem de erro ambígua e pode ser ajustado em um bloco try/catch. A mensagem de erro vista é semelhante à seguinte:  
  
```  
Msg 3994, Level 16, State 1, Procedure uspRollbackFromProc, Line 0  
Transaction is not allowed to roll back inside a user defined routine, trigger or aggregate because the transaction is not started in that CLR level. Change application logic to enforce strict transaction nesting.  
```  
  
 Essa exceção é esperada e o bloco try/catch é necessário para que a execução do código continue. Sem o bloco try/catch, a exceção será gerada imediatamente para o procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)] de chamada e a execução de código gerenciado será concluída. Quando o código gerenciado concluir a execução, outra exceção será gerada:  
  
```  
Msg 3991, Level 16, State 1, Procedure uspRollbackFromProc, Line 1   
The context transaction which was active before entering user defined routine, trigger or aggregate " uspRollbackFromProc " has been ended inside of it, which is not allowed. Change application logic to enforce strict transaction nesting. The statement has been terminated.  
```  
  
 Essa exceção também é esperada e, para que a execução continue, é preciso ter um bloco try/catch em torno da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que executa a ação que aciona o gatilho. Apesar das duas exceções geradas, a transação é revertida e as alterações não são confirmadas.  
  
### <a name="example"></a>Exemplo  
 A seguir, é mostrado um exemplo de uma transação que é revertida de um procedimento gerenciado usando o método **Transaction.Rollback** . Observe o bloco try/catch em torno do método **Transaction.Rollback** no código gerenciado. O script [!INCLUDE[tsql](../../includes/tsql-md.md)] cria um assembly e um procedimento armazenado gerenciado. Lembre-se de que a instrução **EXEC uspRollbackFromProc** é ajustada em um bloco try/catch, de forma que a exceção gerada quando o procedimento gerenciado for concluído seja capturada.  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Transactions;  
  
public partial class StoredProcedures  
{  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void uspRollbackFromProc()  
{  
   using (SqlConnection connection = new SqlConnection(@"context connection=true"))  
   {  
      // Open the connection.  
      connection.Open();  
  
      bool successCondition = true;  
  
      // Success condition is met.  
      if (successCondition)  
      {  
         SqlContext.Pipe.Send("Success condition met in procedure.");   
         // Perform other actions here.  
      }  
  
      //  Success condition is not met, the transaction will be rolled back.  
      else  
      {  
         SqlContext.Pipe.Send("Success condition not met in managed procedure. Transaction rolling back...");  
         try  
         {  
               // Get the current transaction and roll it back.  
               Transaction trans = Transaction.Current;  
               trans.Rollback();  
         }  
         catch (SqlException ex)  
         {  
            // Catch the expected exception.   
            // This allows the connection to close correctly.                      
         }    
      }  
  
      // Close the connection.  
      connection.Close();  
   }  
}  
};  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Transactions  
  
Partial Public Class StoredProcedures  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub  uspRollbackFromProc ()  
   Using connection As New SqlConnection("context connection=true")  
  
   ' Open the connection.  
   connection.Open()  
  
   Dim successCondition As Boolean  
   successCondition = False  
  
   ' Success condition is met.  
   If successCondition Then  
  
      SqlContext.Pipe.Send("Success condition met in procedure.")  
  
      ' Success condition is not met, the transaction will be rolled back.  
  
   Else  
      SqlContext.Pipe.Send("Success condition not met in managed procedure. Transaction rolling back...")  
      Try  
         ' Get the current transaction and roll it back.  
         Dim trans As Transaction  
         trans = Transaction.Current  
         trans.Rollback()  
  
      Catch ex As SqlException  
         ' Catch the exception instead of throwing it.    
         ' This allows the connection to close correctly.                      
      End Try  
  
   End If  
  
   ' Close the connection.  
   connection.Close()  
  
End Using  
End Sub  
End Class  
```  
  
 **Transact-SQL**  
  
```  
--Register assembly.  
CREATE ASSEMBLY TestProcs FROM 'C:\Programming\TestProcs.dll'   
Go  
CREATE PROCEDURE uspRollbackFromProc AS EXTERNAL NAME TestProcs.StoredProcedures.uspRollbackFromProc  
Go  
  
-- Execute procedure.  
BEGIN TRY  
BEGIN TRANSACTION   
-- Perform other actions.  
Exec uspRollbackFromProc  
-- Perform other actions.  
PRINT N'Commiting transaction...'  
COMMIT TRANSACTION  
END TRY  
  
BEGIN CATCH  
SELECT ERROR_NUMBER() AS ErrorNum, ERROR_MESSAGE() AS ErrorMessage  
PRINT N'Exception thrown, rolling back transaction.'  
ROLLBACK TRANSACTION  
PRINT N'Transaction rolled back.'   
END CATCH  
Go  
  
-- Clean up.  
DROP Procedure uspRollbackFromProc;  
Go  
DROP ASSEMBLY TestProcs;  
Go  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Integração CLR e transações](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
