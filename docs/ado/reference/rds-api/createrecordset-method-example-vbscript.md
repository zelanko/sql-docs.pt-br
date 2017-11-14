---
title: "Exemplo do método CreateRecordset (VBScript) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- CreateRecordset method [RDS], VBScript example
ms.assetid: cce0d8b5-e87b-4f7b-a8a0-37d5025a1f5d
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d3ff6c07e6a0198efc0d0e0be23669ebbb9a999b
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="createrecordset-method-example-vbscript"></a>Exemplo do método CreateRecordset (VBScript)
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Este exemplo de código cria um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) no lado do servidor. Ele tem duas colunas com quatro linhas. Recorte e cole o seguinte código ao bloco de notas ou outro editor de texto e salve-o como **CreateRecordsetVBS.asp**.  
  
```  
<!-- BeginCreateRecordsetVBS -->  
<%@ Language=VBScript %>  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>CreateRecordset Method Example (VBScript)</title>  
<style>  
<!--  
body {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
.thead {  
   background-color: #008080;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.thead2 {  
   background-color: #800000;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
    }  
-->  
</style>  
</head>  
  
<body>  
  
<OBJECT classid=clsid:BD96C556-65A3-11D0-983A-00C04FC29E33 height=1 id=DC1 width=1>  
</OBJECT>  
<h1>CreateRecordset Method Example (VBScript)</h1>  
<script language = "vbscript">  
    ' use the RDS.DataControl to create an empty recordset;   
    ' takes an array of variants where every element is itself another  
    ' array of variants, one for every column required in the recordset  
  
    ' the elements of the inner array are the column's  
    ' name, type, size, and nullability  
Sub GetRS()  
   Dim Record(2)  
   Dim Field1(3)  
   Dim Field2(3)  
   Dim Field3(3)  
  
    ' for each field, specify the name type, size, and nullability  
  
   Field1(0) = "Name"   ' Column name.  
   Field1(1) = CInt(129)   ' Column type.  
   Field1(2) = CInt(40)   ' Column size.  
   Field1(3) = False      ' Nullable?  
  
   Field2(0) = "Age"  
   Field2 (1) = CInt(3)  
   Field2 (2) = CInt(-1)  
   Field2 (3) = True  
  
   Field3 (0) = "DateOfBirth"  
   Field3 (1) = CInt(7)  
   Field3 (2) = CInt(-1)  
   Field3 (3) = True  
  
    ' put all fields into an array of arrays  
   Record(0) = Field1  
   Record(1) = Field2  
   Record(2) = Field3  
  
   Dim NewRs   
   Set NewRS = DC1.CreateRecordset(Record)  
  
   Dim fields(2)  
   fields(0) = Field1(0)  
   fields(1) = Field2(0)  
   fields(2) = Field3(0)  
  
    ' Populate the new recordset with data values.  
   Dim fieldVals(2)  
  
    ' Use AddNew to add the records.  
   fieldVals(0) = "Joe"  
   fieldVals(1) = 5  
   fieldVals(2) = CDate(#1/5/96#)  
   NewRS.AddNew fields, fieldVals  
  
   fieldVals(0) = "Mary"  
   fieldVals(1) = 6  
   fieldVals(2) = CDate(#6/5/94#)  
   NewRS.AddNew fields, fieldVals  
  
   fieldVals(0) = "Alex"  
   fieldVals(1) = 13  
   fieldVals(2) = CDate(#1/6/88#)  
   NewRS.AddNew fields, fieldVals  
  
   fieldVals(0) = "Susan"  
   fieldVals(1) = 13  
   fieldVals(2) = CDate(#8/6/87#)  
   NewRS.AddNew fields, fieldVals  
  
   NewRS.MoveFirst  
  
    ' Set the newly created and populated Recordset to  
    ' the SourceRecordset property of the  
    ' RDS.DataControl to bind to visual controls  
  
   Set DC1.SourceRecordset = NewRS  
End Sub  
</script>  
<table datasrc="#DC1" align="center">  
<thead>  
<tr id="ColHeaders" class="thead2">  
   <th>Name</th>  
   <th>Age</th>  
    <th>D.O.B.</th>  
</tr>  
</thead>  
<tbody class="tbody">  
<tr>  
   <td><input datafld="Name" size=15 id=text1 name=text1> </td>  
   <td><input datafld="Age" size=25 id=text2 name=text2> </td>  
   <td><input datafld="DateOfBirth" size=25 id=text3 name=text3> </td>  
</tr>  
</tbody>  
</table>  
<input type = "button" onclick = "GetRS()" value="Go!">  
</body>  
</html>  
<!-- EndCreateRecordsetVBS -->  
```  
  
## <a name="see-also"></a>Consulte também  
 [Método CreateRecordset (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)



