---
title: Executando consultas XPath com namespaces (classes gerenciadas SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 884ea584ec54425d6d0ed2d134e9181cd4d56678
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909216"
---
# <a name="executing-xpath-queries-with-namespaces-sqlxml-managed-classes"></a>Executando consultas XPath com namespaces (classes gerenciadas SQLXML)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  As consultas XPath podem incluir namespaces. Se os elementos de esquema forem qualificados por namespace (use um namespace de destino), as consultas XPath no esquema deverão especificar o namespace.  
  
 Como o caractere curinga (*) não é suportado no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0, você precisa especificar a consulta XPath usando um prefixo de namespace. Para resolver o prefixo, use a propriedade namespaces para especificar a associação de namespace.  
  
 No exemplo a seguir, a consulta XPath especifica namespaces usando o caractere curinga (\*) e as funções XPath de nome local () e namespace-URI (). Essa consulta XPath retorna todos os elementos em que o nome local é **Employee** e o URI do namespace é **urn: MySchema: Contacts**:  
  
```  
/*[local-name() = 'Contact' and namespace-uri() = 'urn:myschema:Contacts']  
```  
  
 No SQLXML 4.0, especifique essa consulta XPath com um prefixo de namespace. Um exemplo é **x:contact**, em que **x** é o prefixo do namespace. Considere o esquema XSD a seguir:  
  
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
  
 O exemplo de aplicativo C# a seguir executa uma consulta XPath com relação ao esquema XSD anterior (MySchema.xml). Para resolver o prefixo, especifique a associação de namespace usando a propriedade namespaces do objeto SqlXmlCommand.  
  
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

