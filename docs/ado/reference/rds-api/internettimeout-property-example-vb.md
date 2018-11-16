---
title: Exemplo da propriedade InternetTimeout (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- InternetTimeout property [ADO], Visual Basic example
ms.assetid: b35d2f4a-449c-4170-aab6-9ff88c890043
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe7074c592c837d292257bcaa18f3eb0638a6515
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606716"
---
# <a name="internettimeout-property-example-vb"></a>Exemplo da propriedade InternetTimeout (VB)
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Este exemplo demonstra a [InternetTimeout](../../../ado/reference/rds-api/internettimeout-property-rds.md) propriedade, que existe na [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) e [DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objetos. Este exemplo usa o **DataControl** de objeto e define o tempo de limite de 20 segundos.  
  
```  
'BeginInternetTimeoutVB  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim dc As RDS.DataControl  
    Dim rst As ADODB.Recordset  
    Set dc = New RDS.DataControl  
  
    dc.Server = "https://MyServer"  
    dc.ExecuteOptions = 1  
    dc.FetchOptions = 1  
    dc.Connect = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    dc.SQL = "SELECT * FROM Authors"  
     ' Wait at least 20 seconds  
    dc.InternetTimeout = 200  
  
    dc.Refresh  
     ' Use another Recordset as a convenience  
    Set rst = dc.Recordset  
    Do While Not rst.EOF  
       Debug.Print rst!au_fname & " " & rst!au_lname  
       rst.MoveNext  
    Loop  
  
    If rst.State = adStateOpen Then rst.Close  
    Set rst = Nothing  
    Set dc = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rst Is Nothing Then  
        If rst.State = adStateOpen Then rst.Close  
    End If  
    Set rst = Nothing  
    Set dc = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
'EndInternetTimeoutVB  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [Propriedade InternetTimeout (RDS)](../../../ado/reference/rds-api/internettimeout-property-rds.md)


