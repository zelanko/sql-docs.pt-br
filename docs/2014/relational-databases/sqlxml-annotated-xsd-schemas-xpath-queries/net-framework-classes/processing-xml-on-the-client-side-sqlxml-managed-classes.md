---
title: Processando XML no lado do cliente (classes gerenciadas SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- processing XML on client side [SQLXML]
- client-side XML formatting
- Managed Classes [SQLXML], client-side XML formatting
- SQLXML Managed Classes, client-side XML formatting
- ClientSideXml property
ms.assetid: 5e7ecf18-66fc-49ff-bc50-83635cd7ac0b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a75d9fb1d4f77cb41cfdc3578af675533fbb6bca
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66010805"
---
# <a name="processing-xml-on-the-client-side-sqlxml-managed-classes"></a>Processando XML no cliente (classes gerenciadas SQLXML)
  Este exemplo ilustra o uso da propriedade ClientSideXml. O aplicativo executa um procedimento armazenado no servidor. O resultado do procedimento armazenado (um conjunto de linhas de duas colunas) é processado no cliente para gerar um documento XML.  
  
 O procedimento armazenado GetContacts a seguir retorna **FirstName** e **LastName** de employees na tabela Person. Contact no banco de dados AdventureWorks.  
  
```  
USE AdventureWorks  
CREATE PROCEDURE GetContacts @LastName varchar(20)  
AS  
SELECT FirstName, LastName  
FROM   Person.Contact  
WHERE LastName = @LastName  
Go  
```  
  
 Este aplicativo C# executa o procedimento armazenado e especifica a opção FOR XML AUTO ao especificar o valor CommandText. No aplicativo, a propriedade ClientSideXml do objeto SqlXmlCommand é definida como true. Isto permite executar procedimentos armazenados pré-existentes que retornam um conjunto de linhas e aplicam uma transformação XML a ele no cliente.  
  
> [!NOTE]  
>  No código, é necessário fornecer o nome da instância do Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na cadeia de conexão.  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
    static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
      public static int testParams()  
      {  
         //Stream strm;  
         SqlXmlParameter p;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.ClientSideXml = true;  
         cmd.CommandText = "EXEC GetContacts ? FOR XML NESTED";  
         p = cmd.CreateParameter();  
         p.Value = "Achong";  
         using (Stream strm = cmd.ExecuteStream())   
         {  
            using (StreamReader sr = new StreamReader(strm))  
                  {  
               Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
         return 0;  
      }  
  
public static int Main(String[] args)  
{  
    testParams();  
    return 0;  
}  
}  
```  
  
 Para testar este exemplo, é necessário ter o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework instalado no computador.  
  
### <a name="to-test-the-application"></a>Para testar o aplicativo  
  
1.  Crie o procedimento armazenado.  
  
2.  Salve o código C# (DocSample.cs) fornecido neste exemplo em uma pasta. Edite o código para especificar as informações de logon e senha apropriadas.  
  
3.  Compile o código. Para compilar o código no prompt de comando, use:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     Isso cria um executável (DocSample.exe).  
  
4.  No prompt de comando, execute DocSample.exe.  
  
  
