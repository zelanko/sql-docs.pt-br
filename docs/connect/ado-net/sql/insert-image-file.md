---
title: Inserindo uma imagem de um arquivo
description: Descreve como trabalhar com uma imagem de um arquivo.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 35900aa2-5615-4174-8212-ba184c6b82fb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: ee951094ad3042e1d2fa31bdf35fa7e5b32f1d2c
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924354"
---
# <a name="inserting-an-image-from-a-file"></a>Inserindo uma imagem de um arquivo

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Você pode gravar um BLOB (objeto binário grande) em um banco de dados como dados binários ou de caractere, dependendo do tipo de campo na fonte de dados. BLOB é um termo genérico que se refere aos tipos de dados `text`, `ntext` e `image`, que normalmente contêm documentos e imagens.  
  
Para gravar um valor de BLOB no banco de dados, emita a instrução INSERT ou UPDATE apropriada e passe o valor de BLOB como um parâmetro de entrada. Se o BLOB for armazenado como texto, como um campo `text` do SQL Server, você poderá passá-lo como um parâmetro de cadeia de caracteres. Se o BLOB for armazenado em formato binário, como um campo `image` do SQL Server, você poderá passar uma matriz do tipo `byte` como um parâmetro binário.
  
## <a name="example"></a>Exemplo  
O exemplo de código a seguir adiciona informações de funcionário à tabela Funcionários no banco de dados da Northwind. Uma foto do funcionário é lida de um arquivo e adicionada ao campo Foto na tabela, que é um campo de imagem.  
  
```csharp  
public static void AddEmployee(  
  string lastName,   
  string firstName,   
  string title,   
  DateTime hireDate,   
  int reportsTo,   
  string photoFilePath,   
  string connectionString)  
{  
  byte[] photo = GetPhoto(photoFilePath);  
  
  using (SqlConnection connection = new SqlConnection(  
    connectionString))  
  
  SqlCommand command = new SqlCommand(  
    "INSERT INTO Employees (LastName, FirstName, " +  
    "Title, HireDate, ReportsTo, Photo) " +  
    "Values(@LastName, @FirstName, @Title, " +  
    "@HireDate, @ReportsTo, @Photo)", connection);   
  
  command.Parameters.Add("@LastName",    
     SqlDbType.NVarChar, 20).Value = lastName;  
  command.Parameters.Add("@FirstName",   
      SqlDbType.NVarChar, 10).Value = firstName;  
  command.Parameters.Add("@Title",       
      SqlDbType.NVarChar, 30).Value = title;  
  command.Parameters.Add("@HireDate",   
       SqlDbType.DateTime).Value = hireDate;  
  command.Parameters.Add("@ReportsTo",   
      SqlDbType.Int).Value = reportsTo;  
  
  command.Parameters.Add("@Photo",  
      SqlDbType.Image, photo.Length).Value = photo;  
  
  connection.Open();  
  command.ExecuteNonQuery();  
  }  
}  
  
public static byte[] GetPhoto(string filePath)  
{  
  FileStream stream = new FileStream(  
      filePath, FileMode.Open, FileAccess.Read);  
  BinaryReader reader = new BinaryReader(stream);  
  
  byte[] photo = reader.ReadBytes((int)stream.Length);  
  
  reader.Close();  
  stream.Close();  
  
  return photo;  
}  
```  
  
## <a name="next-steps"></a>Próximas etapas
- [Dados binários e de valor grande do SQL Server](sql-server-binary-large-value-data.md)
