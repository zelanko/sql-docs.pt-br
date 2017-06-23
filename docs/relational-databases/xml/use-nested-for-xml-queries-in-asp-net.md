---
title: Usar consultas FOR XML aninhadas no ASP.NET | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR XML clause, nested FOR XML queries
- queries [XML in SQL Server], ASP.NET and
- nested FOR XML queries in ASP.NET
- ASP.NET [SQL Server]
ms.assetid: 691ac7dd-afc5-4760-932c-2b1dcd9394ed
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: c0e55c0e35039490f0ce4cd8a7fb6d7e232c05aa
ms.openlocfilehash: 080c4c94b10836dd58206ebf690ea45a946994b0
ms.contentlocale: pt-br
ms.lasthandoff: 06/23/2017

---
# <a name="use-nested-for-xml-queries-in-aspnet"></a>Usar consultas FOR XML aninhadas no ASP.NET
  Neste exemplo, um aplicativo ASP.NET retorna XML a um navegador executando um procedimento armazenado no SQL Server. O procedimento armazenado gera XML usando consultas aninhadas. Uma instrução SELECT semelhante é mostrada no tópico [Gerando irmãos usando uma consulta aninhada em modo AUTO](../../relational-databases/xml/generate-siblings-with-a-nested-auto-mode-query.md). Este exemplo demonstra uma maneira de usar consultas FOR XML aninhadas para gerar XML centrado em elemento no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Exemplo  
  
```  
CREATE PROC GetSalesOrderInfo AS  
SELECT   
      (SELECT top 2 SalesOrderID, SalesPersonID, CustomerID,  
         (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
           from Sales.SalesOrderDetail  
            WHERE  SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
            FOR XML AUTO, TYPE)  
      FROM  Sales.SalesOrderHeader  
        WHERE SalesOrderHeader.SalesOrderID = SalesOrder.SalesOrderID  
      for xml auto, type),  
        (SELECT *   
         FROM  (SELECT SalesPersonID, EmployeeID  
              FROM Sales.SalesPerson, HumanResources.Employee  
              WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
         WHERE  SalesPerson.SalesPersonID = SalesOrder.SalesPersonID  
       FOR XML AUTO, TYPE, ELEMENTS)  
FROM (SELECT SalesOrderHeader.SalesOrderID, SalesOrderHeader.SalesPersonID  
      FROM Sales.SalesOrderHeader, Sales.SalesPerson  
      WHERE SalesOrderHeader.SalesPersonID = SalesPerson.SalesPersonID  
     ) as SalesOrder  
ORDER BY SalesOrder.SalesOrderID  
FOR XML AUTO, TYPE  
GO  
```  
  
 Este é o aplicativo .aspx. Ele executa o procedimento armazenado e retorna XML no navegador:  
  
```  
<%@LANGUAGE=C# Debug=true %>  
<%@import Namespace="System.Xml"%>  
<%@import namespace="System.Data.SqlClient" %><%  
Response.Expires = -1;  
Response.ContentType = "text/xml";  
%>  
  
<%  
using(System.Data.SqlClient.SqlConnection c = new System.Data.SqlClient.SqlConnection("Data Source=server;Database=AdventureWorks;Integrated Security=SSPI;"))  
using(System.Data.SqlClient.SqlCommand cmd = c.CreateCommand())  
{  
   cmd.CommandText = "GetSalesOrderInfo";  
   cmd.CommandType = CommandType.StoredProcedure;  
   cmd.Connection.Open();  
   System.Xml.XmlReader r = cmd.ExecuteXmlReader();  
   System.Xml.XmlTextWriter w = new System.Xml.XmlTextWriter(Response.Output);  
   w.WriteStartElement("Root");  
   r.MoveToContent();  
   while(! r.EOF)  
   {  
      w.WriteNode(r, true);  
   }  
   w.WriteEndElement();  
   w.Flush();  
}  
%>  
```  
  
##### <a name="to-test-the-application"></a>Para testar o aplicativo  
  
1.  Crie o procedimento armazenado no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
2.  Salve o aplicativo .aspx no diretório c:\inetpub\wwwroot (GetSalesOrderInfo.aspx).  
  
3.  Execute o aplicativo (`http://server/GetSalesOrderInfo.aspx`).  
  
## <a name="see-also"></a>Consulte também  
 [Usar consultas FOR XML aninhadas](../../relational-databases/xml/use-nested-for-xml-queries.md)  
  
  
