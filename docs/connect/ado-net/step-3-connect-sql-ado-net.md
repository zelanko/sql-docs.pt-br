---
title: 'Etapa 3: Prova de conceito da conexão com o SQL usando o ADO.NET | Microsoft Docs'
description: Contém exemplos de código C# para se conectar ao SQL Server, executar uma consulta e inserir uma linha.
ms.custom: ''
ms.date: 08/15/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: aebe3dc6-3ee4-4d11-8e43-5d32b3f91490
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: e78ba27912452562199a3d0c4d0d995b17371a56
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80918183"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-adonet"></a>Etapa 3: Prova de conceito da conexão ao SQL usando ADO.NET

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

- Artigo anterior:&nbsp;&nbsp;&nbsp;[Etapa 2: Criar um Banco de Dados SQL para o desenvolvimento no ADO.NET](step-2-create-sql-database-ado-net-development.md)  
- Próximo artigo:&nbsp;&nbsp;&nbsp;[Etapa 4: Conectar-se de modo resiliente ao SQL com ADO.NET](step-4-connect-resiliently-sql-ado-net.md)  

  
Este exemplo de código C# deve ser considerado apenas uma prova de conceito. O código de exemplo está simplificado para fins de clareza e não necessariamente representa as melhores práticas recomendadas pela Microsoft.  
  
## <a name="step-1-connect"></a>Etapa 1: Conectar
  
O método **SqlConnection.Open** é usado para se conectar ao Banco de Dados SQL.  


```csharp
// C# , ADO.NET  
using System;
using QC = Microsoft.Data.SqlClient;  // System.Data.dll  
  
namespace ProofOfConcept_SQL_CSharp  
{  
    public class Program  
    {  
        static public void Main()  
        {  
            using (var connection = new QC.SqlConnection(  
                "Server=tcp:YOUR_SERVER_NAME_HERE.database.windows.net,1433;" +
                "Database=AdventureWorksLT;User ID=YOUR_LOGIN_NAME_HERE;" +
                "Password=YOUR_PASSWORD_HERE;Encrypt=True;" +
                "TrustServerCertificate=False;Connection Timeout=30;"  
                ))  
            {  
                connection.Open();  
                Console.WriteLine("Connected successfully.");  

                Console.WriteLine("Press any key to finish...");  
                Console.ReadKey(true);  
            }  
        }  
    }  
}  
/**** Actual output:  
Connected successfully.  
Press any key to finish...  
****/  
```  


## <a name="step-2-execute-a-query"></a>Etapa 2: Executar uma consulta  
  
O método SqlCommand.ExecuteReader:  
  
- Emite a instrução SQL SELECT para o sistema SQL.  
- Retorna uma instância de SqlDataReader para fornecer acesso às linhas de resultado.  
  
  
  
```csharp
using System;  // C# , ADO.NET  
using DT = System.Data;            // System.Data.dll  
using QC = Microsoft.Data.SqlClient;  // System.Data.dll  
  
namespace ProofOfConcept_SQL_CSharp  
{  
    public class Program  
    {  
        static public void Main()  
        {  
            using (var connection = new QC.SqlConnection(  
                "Server=tcp:YOUR_SERVER_NAME_HERE.database.windows.net,1433;" +
                "Database=AdventureWorksLT;User ID=YOUR_LOGIN_NAME_HERE;" +
                "Password=YOUR_PASSWORD_HERE;Encrypt=True;" +
                "TrustServerCertificate=False;Connection Timeout=30;"  
                ))  
            {  
                connection.Open();  
                Console.WriteLine("Connected successfully.");  
  
                Program.SelectRows(connection);  
  
                Console.WriteLine("Press any key to finish...");  
                Console.ReadKey(true);  
            }  
        }  
  
        static public void SelectRows(QC.SqlConnection connection)  
        {  
            using (var command = new QC.SqlCommand())  
            {  
                command.Connection = connection;  
                command.CommandType = DT.CommandType.Text;  
                command.CommandText = @"  
SELECT  
    TOP 5  
        COUNT(soh.SalesOrderID) AS [OrderCount],  
        c.CustomerID,  
        c.CompanyName  
    FROM  
                        SalesLT.Customer         AS c  
        LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh  
            ON c.CustomerID = soh.CustomerID  
    GROUP BY  
        c.CustomerID,  
        c.CompanyName  
    ORDER BY  
        [OrderCount] DESC,  
        c.CompanyName; ";  
  
                QC.SqlDataReader reader = command.ExecuteReader();  
  
                while (reader.Read())  
                {  
                    Console.WriteLine("{0}\t{1}\t{2}",  
                        reader.GetInt32(0),  
                        reader.GetInt32(1),  
                        reader.GetString(2));  
                }  
            }  
        }  
    }  
}  
/**** Actual output:  
Connected successfully.  
1       29736   Action Bicycle Specialists  
1       29638   Aerobic Exercise Company  
1       29546   Bulk Discount Store  
1       29741   Central Bicycle Specialists  
1       29612   Channel Outlet  
Press any key to finish...  
****/  
```  
  
  
  
## <a name="step-3-insert-a-row"></a>Etapa 3: Inserir uma linha  
  
  
Este exemplo demonstra como:  
  
- Executar uma instrução SQL INSERT com segurança passando parâmetros.  
  - O uso de parâmetros protege contra ataques de injeção de SQL.  
- Recuperar o valor gerado automaticamente.  
  
  
  
```csharp
using System;  // C# , ADO.NET  
using DT = System.Data;            // System.Data.dll  
using QC = Microsoft.Data.SqlClient;  // System.Data.dll  
  
namespace ProofOfConcept_SQL_CSharp  
{  
    public class Program  
    {  
        static public void Main()  
        {  
            using (var connection = new QC.SqlConnection(  
                "Server=tcp:YOUR_SERVER_NAME_HERE.database.windows.net,1433;" +
                "Database=AdventureWorksLT;User ID=YOUR_LOGIN_NAME_HERE;" +
                "Password=YOUR_PASSWORD_HERE;Encrypt=True;" +
                "TrustServerCertificate=False;Connection Timeout=30;"  
                ))  
            {  
                connection.Open();  
                Console.WriteLine("Connected successfully.");  
  
                Program.InsertRows(connection);  
  
                Console.WriteLine("Press any key to finish...");  
                Console.ReadKey(true);  
            }  
        }  
  
        static public void InsertRows(QC.SqlConnection connection)  
        {  
            QC.SqlParameter parameter;  
  
            using (var command = new QC.SqlCommand())  
            {  
                command.Connection = connection;  
                command.CommandType = DT.CommandType.Text;  
                command.CommandText = @"  
INSERT INTO SalesLT.Product  
        (Name,  
        ProductNumber,  
        StandardCost,  
        ListPrice,  
        SellStartDate  
        )  
    OUTPUT  
        INSERTED.ProductID  
    VALUES  
        (@Name,  
        @ProductNumber,  
        @StandardCost,  
        @ListPrice,  
        CURRENT_TIMESTAMP  
        ); ";  
  
                parameter = new QC.SqlParameter("@Name", DT.SqlDbType.NVarChar, 50);  
                parameter.Value = "SQL Server Express 2014";  
                command.Parameters.Add(parameter);  
  
                parameter = new QC.SqlParameter("@ProductNumber", DT.SqlDbType.NVarChar, 25);  
                parameter.Value = "SQLEXPRESS2014";  
                command.Parameters.Add(parameter);  
  
                parameter = new QC.SqlParameter("@StandardCost", DT.SqlDbType.Int);  
                parameter.Value = 11;  
                command.Parameters.Add(parameter);  
  
                parameter = new QC.SqlParameter("@ListPrice", DT.SqlDbType.Int);  
                parameter.Value = 12;  
                command.Parameters.Add(parameter);  
  
                int productId = (int)command.ExecuteScalar();  
                Console.WriteLine("The generated ProductID = {0}.", productId);  
            }  
        }  
    }  
}  
/**** Actual output:  
Connected successfully.  
The generated ProductID = 1000.  
Press any key to finish...  
****/  
```
