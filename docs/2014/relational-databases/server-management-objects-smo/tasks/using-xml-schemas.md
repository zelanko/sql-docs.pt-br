---
title: Usando esquemas XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- XML [SMO]
ms.assetid: 9d04de01-efeb-4b2d-8c28-3234bc7ff2f3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6aee91cdab8ff5404ebb333a81cad91297a99f17
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72781943"
---
# <a name="using-xml-schemas"></a>Usando esquemas XML
  A programação XML no SMO se restringe ao fornecimento de tipos de dados XML, namespaces XML e indexação simples em colunas de tipo de dados XML.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece armazenamento nativo para instâncias de documento XML. Esquemas XML permitem que você defina tipos de dados XML complexos, que podem ser usados para validar documentos XML a fim de garantir a integridade dos dados. O esquema XML é definido no objeto <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection>.  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto Visual Basic Smo no Visual Studio .net](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) ou [criar um projeto&#35; do Visual C Smo no Visual Studio .net](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-an-xml-schema-in-visual-basic"></a>Criando um esquema XML no Visual Basic  
 Este exemplo de código mostra como criar um esquema XML com o objeto <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection>. A propriedade <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A>, que define a coleção de esquemas XML, contém várias aspas duplas. Elas são substituídas pela cadeia de caracteres `chr(34)`.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBXMLSchema1](SMO How to#SMO_VBXMLSchema1)]  -->  
  
## <a name="creating-an-xml-schema-in-visual-c"></a>Criando um esquema XML no Visual C#  
 Este exemplo de código mostra como criar um esquema XML com o objeto <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection>. A propriedade <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A>, que define a coleção de esquemas XML, contém várias aspas duplas. Elas são substituídas pela cadeia de caracteres `chr(34)`.  
  
```csharp
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = default(Server);  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define an XmlSchemaCollection object by supplying the parent  
            // database and name arguments in the constructor.   
            XmlSchemaCollection xsc = default(XmlSchemaCollection);  
            xsc = new XmlSchemaCollection(db, "MySampleCollection");  
            xsc.Text = "<schema xmlns=" + Strings.Chr(34) + "http://www.w3.org/2001/XMLSchema" + Strings.Chr(34) + " xmlns:ns=" + Strings.Chr(34) + "http://ns" + Strings.Chr(34) + "><element name=" + Strings.Chr(34) + "e" + Strings.Chr(34) + " type=" + Strings.Chr(34) + "dateTime" + Strings.Chr(34) + "/></schema>";  
            //Create the XML schema collection on the instance of SQL Server.   
            xsc.Create();  
        }  
```  
  
## <a name="creating-an-xml-schema-in-powershell"></a>Criando um esquema XML no PowerShell  
 Este exemplo de código mostra como criar um esquema XML com o objeto <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection>. A propriedade <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A>, que define a coleção de esquemas XML, contém várias aspas duplas. Elas são substituídas pela cadeia de caracteres `chr(34)`.  
  
```powershell
#Get a server object which corresponds to the default instance replace LocalMachine with the physical server  
cd \sql\LocalHost  
$srv = Get-Item default  
  
#Reference the AdventureWorks database.  
$db = $srv.Databases["AdventureWorks2012"]  
  
#Create a new schema collection  
$xsc = New-Object -TypeName Microsoft.SqlServer.Management.SMO.XmlSchemaCollection `  
-argumentlist $db,"MySampleCollection"  
  
#Add the xml  
$dq = '"' # the double quote character  
$xsc.Text = "<schema xmlns=" + $dq + "http://www.w3.org/2001/XMLSchema" + $dq + `  
"  xmlns:ns=" + $dq + "http://ns" + $dq + "><element name=" + $dq + "e" + $dq +`  
 " type=" + $dq + "dateTime" + $dq + "/></schema>"  
  
#Create the XML schema collection on the instance of SQL Server.  
$xsc.Create()  
```  
