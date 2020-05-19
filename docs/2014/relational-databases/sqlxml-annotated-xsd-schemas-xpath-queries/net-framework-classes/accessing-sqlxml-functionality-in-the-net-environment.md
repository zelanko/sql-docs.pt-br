---
title: Acessando a funcionalidade SQLXML no ambiente .NET | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- Managed Classes [SQLXML], accessing SQLXML functionality
- SQLXML Managed Classes, accessing SQLXML functionality
- DiffGrams [SQLXML], accessing SQLXML functionality
- .NET Framework [SQLXML], accessing SQLXML functionality
ms.assetid: 74744535-2945-414d-9a5b-7e8cc363953a
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a73b983b98e0474f443f3fbcf71b88ad692ac961
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703061"
---
# <a name="accessing-sqlxml-functionality-in-the-net-environment"></a>Acessando a funcionalidade SQLXML no ambiente .NET
  Este exemplo mostra:  
  
-   Como usar [!INCLUDE[msCoName](../../../includes/msconame-md.md)] classes gerenciadas SQLXML (Microsoft. Data. SQLXML) para acessar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a Microsoft no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ambiente de .NET Framework.  
  
-   Como os DiffGrams que são gerados no ambiente .NET Framework podem aplicar atualizações de dados a tabelas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Neste aplicativo, uma consulta XPath é executada em um esquema XSD. A execução da consulta XPath retorna um documento XML que consiste em dados de contato (**FirstName**, **LastName**). O aplicativo carrega o documento XML no conjunto de dados no ambiente .NET Framework. Os dados no conjunto de dados são modificados: o nome do contato é alterado para "Susan", para o primeiro contato no conjunto de dados. O DiffGram é gerado a partir do conjunto de dados, e a atualização que é especificada no DiffGram (a alteração do nome do funcionário) é então aplicada à tabela Person.Contact.  
  
> [!NOTE]  
>  No código, é necessário fornecer o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na cadeia de conexão.  
  
```  
using System;  
using System.Data;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
   static string ConnString = "Provider=SQLOLEDB;Server=SqlServerName;database=AdventureWorks;Integrated Security=SSPI;";  
   public static int testParams()  
   {  
      DataRow row;  
      SqlXmlAdapter ad;  
      //need a memory stream to hold diff gram temporarily  
      MemoryStream ms = new MemoryStream();  
      SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
      cmd.RootTag = "ROOT";  
      cmd.CommandText = "Con";  
      cmd.CommandType = SqlXmlCommandType.XPath;  
      cmd.SchemaPath = "MySchema.xml";  
      //load data set  
      DataSet ds = new DataSet();  
      ad = new SqlXmlAdapter(cmd);  
      ad.Fill(ds);  
      row = ds.Tables["Con"].Rows[0];  
      row["FName"] = "Susan";  
      ad.Update(ds);  
      return 0;  
   }  
   public static int Main(String[] args)  
   {  
      testParams();  
      return 0;  
   }  
}  
```  
  
 **Para testar o exemplo:**  
  
 Para testar este exemplo, é necessário ter o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework instalado no computador.  
  
1.  Salve este esquema XSD (MySchema.xml) em uma pasta:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="Con" sql:relation="Person.Contact" >  
       <xsd:complexType>  
         <xsd:sequence>  
            <xsd:element name="FName"    
                         sql:field="FirstName"   
                         type="xsd:string" />   
            <xsd:element name="LName"    
                         sql:field="LastName"    
                         type="xsd:string" />  
         </xsd:sequence>  
         <xsd:attribute name="ContactID" type="xsd:integer" />  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
2.  Salve o código C# (DocSample.cs) fornecido neste exemplo na mesma pasta na qual o esquema está armazenado. (Se você armazenar os arquivos em pastas diferentes, terá que editar o código e especificar o caminho de diretório apropriado para o esquema de mapeamento.)  
  
3.  Compile o código. Para compilar o código no prompt de comando, use:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     Isso cria um executável (DocSample.exe).  
  
 No prompt de comando, execute DocSample.exe.  
  
  
