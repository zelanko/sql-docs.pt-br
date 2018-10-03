---
title: Usando esquemas XML | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- XML [SMO]
ms.assetid: 9d04de01-efeb-4b2d-8c28-3234bc7ff2f3
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d0e6c33529219e73b4d517dc23fc933b0bf31f1c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47814174"
---
# <a name="using-xml-schemas"></a>Usando esquemas XML
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  A programação XML no SMO se restringe ao fornecimento de tipos de dados XML, namespaces XML e indexação simples em colunas de tipo de dados XML.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Fornece armazenamento nativo para instâncias de documento XML. Esquemas XML permitem que você defina tipos de dados XML complexos, que podem ser usados para validar documentos XML a fim de garantir a integridade dos dados. O esquema XML é definido no objeto <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection>.  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um Visual C&#35; projeto do SMO no Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-an-xml-schema-in-visual-basic"></a>Criando um esquema XML no Visual Basic  
 Este exemplo de código mostra como criar um esquema XML com o objeto <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection>. A propriedade <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A>, que define a coleção de esquemas XML, contém várias aspas duplas. Elas são substituídas pela cadeia de caracteres `chr(34)`.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server()
'Reference the AdventureWorks2012 2008R2 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define an XmlSchemaCollection object by supplying the parent database and name arguments in the constructor.
Dim xsc As XmlSchemaCollection
xsc = New XmlSchemaCollection(db, "MySampleCollection")
xsc.Text = "\<schema xmlns=" + Chr(34) + "http://www.w3.org/2001/XMLSchema" + Chr(34) + "  xmlns:ns=" + Chr(34) + "http://ns" + Chr(34) + ">\<element name=" + Chr(34) + "e" + Chr(34) + " type=" + Chr(34) + "dateTime" + Chr(34) + "/></schema>"
'Create the XML schema collection on the instance of SQL Server.
xsc.Create()
```
  
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
            xsc.Text = "\<schema xmlns=" + Strings.Chr(34) + "http://www.w3.org/2001/XMLSchema" + Strings.Chr(34) + " xmlns:ns=" + Strings.Chr(34) + "http://ns" + Strings.Chr(34) + ">\<element name=" + Strings.Chr(34) + "e" + Strings.Chr(34) + " type=" + Strings.Chr(34) + "dateTime" + Strings.Chr(34) + "/></schema>";  
            //Create the XML schema collection on the instance of SQL Server.   
            xsc.Create();  
        }  
```  
  
## <a name="creating-an-xml-schema-in-powershell"></a>Criando um esquema XML no PowerShell  
 Este exemplo de código mostra como criar um esquema XML com o objeto <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection>. A propriedade <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A>, que define a coleção de esquemas XML, contém várias aspas duplas. Elas são substituídas pela cadeia de caracteres `chr(34)`.  
  
```powershell   
#Get a server object which corresponds to the default instance replace LocalMachine with the physical server  
cd \sql\LocalHost  
$srv = get-item default  
  
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
  
  
