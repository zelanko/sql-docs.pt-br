---
title: Manipulando dados
description: Fornece exemplos de aplicativos de codificação MARS.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 51096a2e-8b38-4c4d-a523-799bfdb7ec69
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: df430bbacb69e1d95d001e4f9340ca60473503cd
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452167"
---
# <a name="manipulating-data"></a>Manipulando dados

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Antes da introdução de MARS (vários conjuntos de resultados ativos), os desenvolvedores precisavam usar várias conexões ou cursores do lado do servidor para resolver determinados cenários. Além disso, quando várias conexões eram usadas em uma situação transacional, as conexões associadas (com **sp_getbindtoken** e **sp_bindsession**) eram necessárias. Os cenários a seguir mostram como usar uma conexão habilitada para MARS em vez de várias conexões.  
  
## <a name="using-multiple-commands-with-mars"></a>Usando vários comandos com MARS  
O aplicativo de console a seguir demonstra como usar dois objetos <xref:Microsoft.Data.SqlClient.SqlDataReader> com dois objetos <xref:Microsoft.Data.SqlClient.SqlCommand> e um único objeto <xref:Microsoft.Data.SqlClient.SqlConnection> com o MARS habilitado.  
  
### <a name="example"></a>Exemplo  
O exemplo abre uma única conexão com o banco de dados **AdventureWorks** . Usando um objeto <xref:Microsoft.Data.SqlClient.SqlCommand>, um <xref:Microsoft.Data.SqlClient.SqlDataReader> é criado. Conforme o leitor é usado, um segundo <xref:Microsoft.Data.SqlClient.SqlDataReader> é aberto, usando dados da primeira <xref:Microsoft.Data.SqlClient.SqlDataReader> como entrada para a cláusula WHERE para o segundo leitor.  
  
> [!NOTE]
>  O exemplo a seguir usa o banco de dados de exemplo **AdventureWorks** incluído com o SQL Server. A cadeia de conexão fornecida no código de exemplo pressupõe que o banco de dados está instalado e disponível no computador local. Modifique a cadeia de conexão conforme necessário para o seu ambiente.  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
class Class1  
{  
static void Main()  
{  
  // By default, MARS is disabled when connecting  
  // to a MARS-enabled host.  
  // It must be enabled in the connection string.  
  string connectionString = GetConnectionString();  
  
  int vendorID;  
  SqlDataReader productReader = null;  
  string vendorSQL =   
    "SELECT VendorId, Name FROM Purchasing.Vendor";  
  string productSQL =   
    "SELECT Production.Product.Name FROM Production.Product " +  
    "INNER JOIN Purchasing.ProductVendor " +  
    "ON Production.Product.ProductID = " +   
    "Purchasing.ProductVendor.ProductID " +  
    "WHERE Purchasing.ProductVendor.VendorID = @VendorId";  
  
  using (SqlConnection awConnection =   
    new SqlConnection(connectionString))  
  {  
    SqlCommand vendorCmd = new SqlCommand(vendorSQL, awConnection);  
    SqlCommand productCmd =   
      new SqlCommand(productSQL, awConnection);  
  
    productCmd.Parameters.Add("@VendorId", SqlDbType.Int);  
  
    awConnection.Open();  
    using (SqlDataReader vendorReader = vendorCmd.ExecuteReader())  
    {  
      while (vendorReader.Read())  
      {  
        Console.WriteLine(vendorReader["Name"]);  
  
        vendorID = (int)vendorReader["VendorId"];  
  
        productCmd.Parameters["@VendorId"].Value = vendorID;  
        // The following line of code requires  
        // a MARS-enabled connection.  
        productReader = productCmd.ExecuteReader();  
        using (productReader)  
        {  
          while (productReader.Read())  
          {  
            Console.WriteLine("  " +  
              productReader["Name"].ToString());  
          }  
        }  
      }  
  }  
      Console.WriteLine("Press any key to continue");  
      Console.ReadLine();  
    }  
  }  
  private static string GetConnectionString()  
  {  
    // To avoid storing the connection string in your code,  
    // you can retrieve it from a configuration file.  
    return "Data Source=(local);Integrated Security=SSPI;" +   
      "Initial Catalog=AdventureWorks;MultipleActiveResultSets=True";  
  }  
}  
```  
  
## <a name="reading-and-updating-data-with-mars"></a>Lendo e atualizando dados com MARS  
O MARS permite que uma conexão seja usada para operações de leitura e de DML (linguagem de manipulação de dados) com mais de uma operação pendente. Esse recurso elimina a necessidade de um aplicativo lidar com erros de conexão. Além disso, o MARS pode substituir o usuário de cursores do lado do servidor, o que geralmente consome mais recursos. Finalmente, como as várias operações podem funcionar em uma única conexão, elas podem compartilhar o mesmo contexto de transação, eliminando a necessidade de usar procedimentos armazenados do sistema **sp_getbindtoken** e **sp_bindsession**.  
  
### <a name="example"></a>Exemplo  
O aplicativo de console a seguir demonstra como usar dois objetos <xref:Microsoft.Data.SqlClient.SqlDataReader> com três objetos <xref:Microsoft.Data.SqlClient.SqlCommand> e um único objeto <xref:Microsoft.Data.SqlClient.SqlConnection> com o MARS habilitado. O primeiro objeto de comando recupera uma lista de fornecedores cuja classificação de crédito é 5. O segundo objeto de comando usa a ID do fornecedor fornecida de um <xref:Microsoft.Data.SqlClient.SqlDataReader> para carregar o segundo <xref:Microsoft.Data.SqlClient.SqlDataReader> com todos os produtos para o fornecedor específico. Cada registro de produto é visitado pela segunda <xref:Microsoft.Data.SqlClient.SqlDataReader>. Um cálculo é executado para determinar o que o novo **OnOrderQty** deve ser. O terceiro objeto de comando é usado para atualizar a tabela **ProductVendor** com o novo valor. Todo esse processo ocorre em uma única transação, que é revertida no final.  
  
> [!NOTE]
>  O exemplo a seguir usa o banco de dados de exemplo **AdventureWorks** incluído com o SQL Server. A cadeia de conexão fornecida no código de exemplo pressupõe que o banco de dados está instalado e disponível no computador local. Modifique a cadeia de conexão conforme necessário para o seu ambiente.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
class Program  
{  
static void Main()  
{  
  // By default, MARS is disabled when connecting  
  // to a MARS-enabled host.  
  // It must be enabled in the connection string.  
  string connectionString = GetConnectionString();  
  
  SqlTransaction updateTx = null;  
  SqlCommand vendorCmd = null;  
  SqlCommand prodVendCmd = null;  
  SqlCommand updateCmd = null;  
  
  SqlDataReader prodVendReader = null;  
  
  int vendorID = 0;  
  int productID = 0;  
  int minOrderQty = 0;  
  int maxOrderQty = 0;  
  int onOrderQty = 0;  
  int recordsUpdated = 0;  
  int totalRecordsUpdated = 0;  
  
  string vendorSQL =  
      "SELECT VendorID, Name FROM Purchasing.Vendor " +   
      "WHERE CreditRating = 5";  
  string prodVendSQL =  
      "SELECT ProductID, MaxOrderQty, MinOrderQty, OnOrderQty " +  
      "FROM Purchasing.ProductVendor " +   
      "WHERE VendorID = @VendorID";  
  string updateSQL =  
      "UPDATE Purchasing.ProductVendor " +   
      "SET OnOrderQty = @OrderQty " +  
      "WHERE ProductID = @ProductID AND VendorID = @VendorID";  
  
  using (SqlConnection awConnection =   
    new SqlConnection(connectionString))  
  {  
    awConnection.Open();  
    updateTx = awConnection.BeginTransaction();  
  
    vendorCmd = new SqlCommand(vendorSQL, awConnection);  
    vendorCmd.Transaction = updateTx;  
  
    prodVendCmd = new SqlCommand(prodVendSQL, awConnection);  
    prodVendCmd.Transaction = updateTx;  
    prodVendCmd.Parameters.Add("@VendorId", SqlDbType.Int);  
  
    updateCmd = new SqlCommand(updateSQL, awConnection);  
    updateCmd.Transaction = updateTx;  
    updateCmd.Parameters.Add("@OrderQty", SqlDbType.Int);  
    updateCmd.Parameters.Add("@ProductID", SqlDbType.Int);  
    updateCmd.Parameters.Add("@VendorID", SqlDbType.Int);  
  
    using (SqlDataReader vendorReader = vendorCmd.ExecuteReader())  
    {  
      while (vendorReader.Read())  
      {  
        Console.WriteLine(vendorReader["Name"]);  
  
        vendorID = (int) vendorReader["VendorID"];  
        prodVendCmd.Parameters["@VendorID"].Value = vendorID;  
        prodVendReader = prodVendCmd.ExecuteReader();  
  
        using (prodVendReader)  
        {  
          while (prodVendReader.Read())  
          {  
            productID = (int) prodVendReader["ProductID"];  
  
            if (prodVendReader["OnOrderQty"] == DBNull.Value)  
            {  
              minOrderQty = (int) prodVendReader["MinOrderQty"];  
              onOrderQty = minOrderQty;  
            }  
            else  
            {  
              maxOrderQty = (int) prodVendReader["MaxOrderQty"];  
              onOrderQty = (int)(maxOrderQty / 2);  
            }  
  
            updateCmd.Parameters["@OrderQty"].Value = onOrderQty;  
            updateCmd.Parameters["@ProductID"].Value = productID;  
            updateCmd.Parameters["@VendorID"].Value = vendorID;  
  
            recordsUpdated = updateCmd.ExecuteNonQuery();  
            totalRecordsUpdated += recordsUpdated;  
          }  
        }  
      }  
    }  
    Console.WriteLine("Total Records Updated: " +   
      totalRecordsUpdated.ToString());  
    updateTx.Rollback();  
    Console.WriteLine("Transaction Rolled Back");  
  }  
  
  Console.WriteLine("Press any key to continue");  
  Console.ReadLine();  
}  
private static string GetConnectionString()  
{  
  // To avoid storing the connection string in your code,  
  // you can retrieve it from a configuration file.  
  return "Data Source=(local);Integrated Security=SSPI;" +   
    "Initial Catalog=AdventureWorks;" +   
    "MultipleActiveResultSets=True";  
  }  
}  
```  
  
## <a name="next-steps"></a>Próximas etapas
- [MARS (conjunto de resultados ativos múltiplos)](multiple-active-result-sets-mars.md)
