---
title: Executando consultas XPath com Namespaces (Classes gerenciadas SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- namespaces property
- XPath queries [SQLXML], SQLXML Managed Classes
- queries [SQLXML], SQLXML Managed Classes
- XPath queries [SQLXML], namespaces
- Managed Classes [SQLXML], executing XPath queries
- SQLXML Managed Classes, executing XPath queries
- namespaces [SQLXML], XPath queries
ms.assetid: c6fc46d8-6b42-4992-a8f1-a8d4b8886e6e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 793107e91425e4fa0df23211a6d4ea42afef8c54
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010798"
---
# <a name="executing-xpath-queries-with-namespaces-sqlxml-managed-classes"></a>Executando consultas XPath com namespaces (classes gerenciadas SQLXML)
  As consultas XPath podem incluir namespaces. Se os elementos de esquema forem qualificados por namespace (use um namespace de destino), as consultas XPath no esquema deverão especificar o namespace.  
  
 Como o caractere curinga (*) não é suportado no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0, você precisa especificar a consulta XPath usando um prefixo de namespace. Para resolver o prefixo, use a propriedade de namespaces para especificar a associação de namespace.  
  
 No exemplo a seguir, a consulta XPath especifica namespaces usando o caractere curinga (\*) e as funções XPath example e namespace-uri(). Essa consulta XPath retorna todos os elementos em que o nome local é `Employee` e o URI de namespace é `urn:myschema:Contacts`:  
  
```  
/*[local-name() = 'Contact' and namespace-uri() = 'urn:myschema:Contacts']  
```  
  
 No SQLXML 4.0, especifique essa consulta XPath com um prefixo de namespace. Um exemplo é `x:Contact`, em que `x` é o prefixo de namespace. Considere o esquema XSD a seguir:  
  
```  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
            xmlns:con="urn:myschema:Contacts"  
            targetNamespace="urn:myschema:Contacts">  
<complexType name="ContactType">  
  <attribute name="CID" sql:field="ContactID" type="ID"/>  
  <attribute name="FName" sql:field="FirstName" type="string"/>  
  <attribute name="LName" sql:field="LastName"/>   
</complexType>  
<element name="Contact" type="con:ContactType" sql:relation="Person.Contact"/>  
</schema>  
```  
  
 Como esse esquema define o namespace de destino, uma consulta XPath (como "Employee") com relação a esse esquema precisa incluir o namespace.  
  
 O exemplo de aplicativo C# a seguir executa uma consulta XPath com relação ao esquema XSD anterior (MySchema.xml). Para resolver o prefixo, especifique a associação de namespace usando a propriedade de Namespaces do objeto SqlXmlCommand.  
  
> [!NOTE]  
>  No código, é necessário fornecer o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na cadeia de conexão.  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
      static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
      public static int testXPath()  
      {  
         //Stream strm;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.CommandText = "x:Contact[@CID='1']";  
         cmd.CommandType = SqlXmlCommandType.XPath;  
         cmd.RootTag = "ROOT";  
         cmd.Namespaces = "xmlns:x='urn:myschema:Contacts'";  
         cmd.SchemaPath = "MySchema.xml";  
         using (Stream strm = cmd.ExecuteStream()){  
            using (StreamReader sr = new StreamReader(strm)){  
               Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
         return 0;  
      }  
      public static int Main(String[] args)  
      {  
         testXPath();  
         return 0;  
      }  
   }  
```  
  
 Para testar este exemplo, é necessário ter o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework instalado no computador.  
  
### <a name="to-test-the-application"></a>Para testar o aplicativo  
  
1.  Salve o esquema XSD (MySchema.xml) que é fornecido neste exemplo em uma pasta.  
  
2.  Salve o código C# (DocSample.cs) fornecido neste exemplo na mesma pasta em que o esquema está armazenado. (Se você armazenar os arquivos em pastas diferentes, terá que editar o código e especificar o caminho de diretório apropriado para o esquema de mapeamento.)  
  
3.  Compile o código. Para compilar o código no prompt de comando, use:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     Isso cria um executável (DocSample.exe).  
  
4.  No prompt de comando, execute DocSample.exe.  
  
  
