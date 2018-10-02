---
title: GET_FILESTREAM_TRANSACTION_CONTEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GET_FILESTREAM_TRANSACTION_CONTEXT_TSQL
- GET_FILESTREAM_TRANSACTION_CONTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- GET_FILESTREAM_TRANSACTION_CONTEXT FILESTREAM [SQL Server]
ms.assetid: 459e6b79-4420-41e6-85bf-89d90f43b4f1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 028390d9eea36ff4dcfd3ffb1fd81a44e9f1daea
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47629015"
---
# <a name="getfilestreamtransactioncontext-transact-sql"></a>GET_FILESTREAM_TRANSACTION_CONTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna um token que representa o contexto da transação atual de uma sessão. O token é usado por um aplicativo para associar operações de fluxo contínuo do sistema de arquivos de FILESTREAM à transação. Para obter uma lista de tópicos de FILESTREAM, confira [Dados de blob &#40;objeto binário grande&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GET_FILESTREAM_TRANSACTION_CONTEXT ()  
```  
  
## <a name="return-type"></a>Tipo de retorno  
 **varbinary(max)**  
  
## <a name="return-value"></a>Valor retornado  
 NULL será retornado se a transação não tiver sido iniciada, ou tiver sido cancelada ou confirmada.  
  
## <a name="remarks"></a>Remarks  
 A transação deve ser explícita. Use BEGIN TRANSACTION seguido por COMMIT TRANSACTION ou ROLLBACK TRANSACTION.  
  
 Quando você chama GET_FILESTREAM_TRANSACTION_CONTEXT, o chamador recebe acesso de sistema de arquivos à transação durante a sua duração. Para permitir que outro usuário acesse a transação pelo sistema de arquivos, use EXECUTE AS para executar GET_FILESTREAM_TRANSACTION_CONTEXT como outro usuário.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `GET_FILESTREAM_TRANSACTION_CONTEXT` em uma transação [!INCLUDE[tsql](../../includes/tsql-md.md)] para obter o contexto da transação.  
  
```csharp  
using System;  
using System.Data.SqlClient;  
using System.Data;  
  
namespace ConsoleApplication  
{  
    /// <summary>  
    /// This class is a wrapper that contains methods for:  
    ///   
    ///     GetTransactionContect() - Returns the current transaction context.  
    ///     BeginTransaction() - Begins a transaction.  
    ///     CommmitTransaction() - Commits the current transaction.  
    ///   
    /// </summary>  
  
    class SqlAccessWrapper  
    {  
        /// <summary>  
        /// Returns a byte array that contains the current transaction  
        /// context.  
        /// </summary>  
        /// <param name="sqlConnection">  
        /// SqlConnection object that represents the instance of SQL Server  
        /// from which to obtain the transaction context.   
        /// </param>  
        /// <returns>  
        /// If there is a current transaction context, the return  
        /// value is an Object that represents the context.  
        /// If there is not a current transaction context, the  
        /// value returned is DBNull.Value.  
        /// </returns>  
  
        public Object GetTransactionContext(SqlConnection sqlConnection)  
        {  
            SqlCommand cmd = new SqlCommand();  
            cmd.CommandText = "SELECT GET_FILESTREAM_TRANSACTION_CONTEXT()";  
            cmd.CommandType = CommandType.Text;  
            cmd.Connection = sqlConnection;  
  
            return cmd.ExecuteScalar();  
  
        }  
  
        /// <summary>  
        /// Begins the transaction.  
        /// </summary>  
        /// <param name="sqlConnection">  
        /// SqlConnection object that represents the server  
        /// on which to run the BEGIN TRANSACTION statement.  
        /// </param>  
  
        public void BeginTransaction(SqlConnection sqlConnection)  
        {  
            SqlCommand cmd = new SqlCommand();  
  
            cmd.CommandText = "BEGIN TRANSACTION";  
            cmd.CommandType = CommandType.Text;  
            cmd.Connection = sqlConnection;  
  
            cmd.ExecuteNonQuery();  
        }  
  
        /// <summary>  
        /// Commits the transaction.  
        /// </summary>  
        /// <param name="sqlConnection">  
        /// SqlConnection object that represents the instance of SQL Server  
        /// on which to run the COMMIT statement.  
        /// </param>  
  
        public void CommitTransaction(SqlConnection sqlConnection)  
        {  
            SqlCommand cmd = new SqlCommand();  
  
            cmd.CommandText = "COMMIT TRANSACTION";  
            cmd.CommandType = CommandType.Text;  
            cmd.Connection = sqlConnection;  
  
            cmd.ExecuteNonQuery();  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            //Open a connection to the local instance of SQL Server.  
  
            SqlConnection sqlConnection = new SqlConnection("Integrated Security=true;server=(local)");  
            sqlConnection.Open();  
  
            SqlAccessWrapper sql = new SqlAccessWrapper();  
  
            //Create a transaction so that sql.GetTransactionContext() will succeed.  
            sql.BeginTransaction(sqlConnection);  
  
            //The transaction context will be stored in this array.  
            Byte[] transactionToken;     
  
            Object txObj = sql.GetTransactionContext(sqlConnection);  
            if (DBNull.Value != txObj)  
            {  
                transactionToken = (byte[])txObj;  
                Console.WriteLine("Transaction context obtained.\n");  
            }  
  
            sql.CommitTransaction(sqlConnection);  
        }  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data.SqlClient  
Imports System.Data  
  
Namespace ConsoleApplication  
    ''' <summary>   
    ''' This class is a wrapper that contains methods for:   
    '''   
    ''' GetTransactionContect() - Returns the current transaction context.   
    ''' BeginTransaction() - Begins a transaction.   
    ''' CommmitTransaction() - Commits the current transaction.   
    '''   
    ''' </summary>   
  
    Class SqlAccessWrapper  
        ''' <summary>   
        ''' Returns a byte array that contains the current transaction   
        ''' context.   
        ''' </summary>   
        ''' <param name="sqlConnection">   
        ''' SqlConnection object that represents the instance of SQL Server   
        ''' from which to obtain the transaction context.   
        ''' </param>   
        ''' <returns>   
        ''' If there is a current transaction context, the return   
        ''' value is an Object that represents the context.   
        ''' If there is not a current transaction context, the   
        ''' value returned is DBNull.Value.   
        ''' </returns>   
  
        Public Function GetTransactionContext(ByVal sqlConnection As SqlConnection) As Object  
            Dim cmd As New SqlCommand()  
            cmd.CommandText = "SELECT GET_FILESTREAM_TRANSACTION_CONTEXT()"  
            cmd.CommandType = CommandType.Text  
            cmd.Connection = sqlConnection  
  
            Return cmd.ExecuteScalar()  
  
        End Function  
  
        ''' <summary>   
        ''' Begins the transaction.   
        ''' </summary>   
        ''' <param name="sqlConnection">   
        ''' SqlConnection object that represents the server   
        ''' on which to run the BEGIN TRANSACTION statement.   
        ''' </param>   
  
        Public Sub BeginTransaction(ByVal sqlConnection As SqlConnection)  
            Dim cmd As New SqlCommand()  
  
            cmd.CommandText = "BEGIN TRANSACTION"  
            cmd.CommandType = CommandType.Text  
            cmd.Connection = sqlConnection  
  
            cmd.ExecuteNonQuery()  
        End Sub  
  
        ''' <summary>   
        ''' Commits the transaction.   
        ''' </summary>   
        ''' <param name="sqlConnection">   
        ''' SqlConnection object that represents the instance of SQL Server   
        ''' on which to run the COMMIT statement.   
        ''' </param>   
  
        Public Sub CommitTransaction(ByVal sqlConnection As SqlConnection)  
            Dim cmd As New SqlCommand()  
  
            cmd.CommandText = "COMMIT TRANSACTION"  
            cmd.CommandType = CommandType.Text  
            cmd.Connection = sqlConnection  
  
            cmd.ExecuteNonQuery()  
        End Sub  
    End Class  
  
    Class Program  
        Shared Sub Main()  
            '''Open a connection to the local instance of SQL Server.  
  
            Dim sqlConnection As New SqlConnection("Integrated Security=true;server=(local)")  
            sqlConnection.Open()  
  
            Dim sql As New SqlAccessWrapper()  
  
            '''Create a transaction so that sql.GetTransactionContext() will succeed.   
            sql.BeginTransaction(sqlConnection)  
  
            '''The transaction context will be stored in this array.   
            Dim transactionToken As Byte()  
  
            Dim txObj As Object = sql.GetTransactionContext(sqlConnection)  
  
            '''If the returned object is not NULL, there is a valid transaction  
            '''token, and it must be converted into a format that is usable within  
            '''the application.  
  
            If Not txObj.Equals(DBNull.Value) Then  
                transactionToken = DirectCast(txObj, Byte())  
                Console.WriteLine("Transaction context obtained." & Chr(10) & "")  
            End If  
  
            sql.CommitTransaction(sqlConnection)  
        End Sub  
    End Class  
End Namespace  
```  
  
## <a name="see-also"></a>Consulte Também  
 [PathName &#40;Transact-SQL&#41;](../../relational-databases/system-functions/pathname-transact-sql.md)   
 [Objeto binário grande &#40;Blob&#41; Dados &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)  
  
  
