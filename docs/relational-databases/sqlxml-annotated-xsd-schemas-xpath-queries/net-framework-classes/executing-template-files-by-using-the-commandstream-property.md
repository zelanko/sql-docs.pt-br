---
title: Executando arquivos de modelo usando a propriedade CommandStream | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Managed Classes [SQLXML], executing template files
- SQLXML Managed Classes, executing template files
- templates [SQLXML], SQLXML Managed Classes
- CommandStream property
ms.assetid: 55c564e3-56d1-4d85-bcaa-703e2905dd57
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d51834522bf6f6d3b8e3243340406d95376aac54
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38051534"
---
# <a name="executing-template-files-by-using-the-commandstream-property"></a>Executando os arquivos de modelo usando a propriedade CommandStream
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Este exemplo ilustra como os arquivos de modelo que consistem em consultas SQL ou XPath podem ser especificados usando a propriedade CommandStream do objeto SqlXmlCommand. Neste aplicativo, um FileStreamobject é aberto para um arquivo de comando, e o fluxo de arquivos é atribuído como o CommandStream que é executado.  
  
 No exemplo a seguir, a propriedade CommandType é especificada como SqlXmlCommandType.Template (não como TemplateFile).  
  
 Este é o modelo XML de exemplo:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>  
    SELECT TOP 2 ContactID, FirstName, LastName   
    FROM   Person.Contact  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 Esse é o aplicativo C# de exemplo. Para testar o aplicativo, salve o modelo (TemplateFile.xml) e execute o aplicativo. O aplicativo executa a consulta especificada no modelo XML e exibe o documento XML gerado na tela.  
  
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
         MemoryStream ms = new MemoryStream();  
         StreamWriter sw = new StreamWriter(ms);  
         ms.Position = 0;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.CommandStream = new FileStream("TemplateFile.xml", FileMode.Open, FileAccess.Read);  
         cmd.CommandType = SqlXmlCommandType.Template;  
         using (Stream strm = cmd.ExecuteStream())  
         {  
            using (StreamReader sr = new StreamReader(strm)){  
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
  
### <a name="to-test-the-application"></a>Para testar o aplicativo  
  
1.  Salve o modelo XML (TemplateFile.xml) fornecido neste exemplo em uma pasta.  
  
2.  Salve o código C# (DocSample.cs) fornecido neste exemplo na mesma pasta em que o esquema está armazenado. (Se você armazenar os arquivos em pastas diferentes, terá que editar o código e especificar o caminho de diretório apropriado para o esquema de mapeamento.)  
  
3.  Compile o código. Para compilar o código no prompt de comando, use:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     Isso cria um executável (DocSample.exe).  
  
4.  No prompt de comando, execute DocSample.exe.  
  
  
