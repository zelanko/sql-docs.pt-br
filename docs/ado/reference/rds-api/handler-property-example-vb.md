---
title: Exemplo da propriedade Handler (VB) | Microsoft Docs
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
- Handler property [ADO], Visual Basic example
ms.assetid: 9664f9a6-65fc-4e7f-be3d-3e4b501b558a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1a72e393716d3d24fdb9f0f95be9faae85651696
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964101"
---
# <a name="handler-property-example-vb"></a>Exemplo da propriedade Handler (VB)
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Este exemplo demonstra a propriedade do [manipulador](../../../ado/reference/rds-api/handler-property-rds.md) de objeto de [DataControl do RDS](../../../ado/reference/rds-api/datacontrol-object-rds.md) . (Consulte [personalização de datafactory](../../../ado/guide/remote-data-service/datafactory-customization.md) para obter mais detalhes.)  
  
 Suponha que as seções a seguir no arquivo de parâmetro, Msdfmap. ini, estejam localizadas no servidor:  
  
```  
[connect AuthorDataBase]  
Access=ReadWrite  
Connect="DSN=Pubs"  
[sql AuthorById]  
SQL="SELECT * FROM Authors WHERE au_id = ?"  
```  
  
 Seu código é semelhante ao seguinte. O comando atribuído à propriedade [SQL](../../../ado/reference/rds-api/sql-property.md) corresponderá ao identificador de ***AuthorById*** e recuperará uma linha para o autor de Michael Leary. A propriedade **Recordset** do objeto **DataControl** é atribuída a um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) desconectado puramente como uma conveniência de codificação.  
  
```  
'BeginHandlerVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim dc As New DataControl  
    Dim rst As ADODB.Recordset  
  
    dc.Handler = "MSDFMAP.Handler"  
    dc.ExecuteOptions = 1  
    dc.FetchOptions = 1  
    dc.Server = "https://MyServer"  
    dc.Connect = "Data Source=AuthorDataBase"  
    dc.SQL = "AuthorById('267-41-2394')"  
    dc.Refresh                  'Retrieve the record  
    Set rst = dc.Recordset      'Use another Recordset as a convenience  
    Debug.Print "Author is '" & rst!au_fname & " " & rst!au_lname & "'"  
  
    ' clean up  
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
'EndHandlerVB  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Propriedade Handler (RDS)](../../../ado/reference/rds-api/handler-property-rds.md)


