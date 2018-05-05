---
title: Adicionar usuários e grupos, exemplo dos métodos ChangePassword (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ChangePassword method [ADOX], Visual Basic example
- Append method [ADOX], Visual Basic example
ms.assetid: c9426757-9cdd-4a95-b506-d3d011569109
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ad64050af9fd606008064c0ff96ab1d90a926bc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="groups-and-users-append-changepassword-methods-example-vb"></a>Adicionar usuários e grupos, exemplo dos métodos ChangePassword (VB)
Este exemplo demonstra o [Append](../../../ado/reference/adox-api/append-method-adox-groups.md) método [grupos](../../../ado/reference/adox-api/groups-collection-adox.md), bem como a [acrescentar](../../../ado/reference/adox-api/append-method-adox-users.md) método de [usuários](../../../ado/reference/adox-api/users-collection-adox.md) adicionando um novo [Grupo](../../../ado/reference/adox-api/group-object-adox.md) e um novo [usuário](../../../ado/reference/adox-api/user-object-adox.md) no sistema. O novo **grupo** é acrescentado ao **grupos** coleção do novo **usuário**. Consequentemente, o novo **usuário** é adicionada para o **grupo**. Além disso, o [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) método é usado para especificar o **usuário** senha.  
  
> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que oferece suporte à autenticação do Windows, você deve especificar **Trusted_Connection = yes** ou **segurança integrada = SSPI** em vez de ID de usuário e senha informações na cadeia de conexão.  
  
```  
' BeginGroupVB  
Sub Main()  
    On Error GoTo GroupXError  
  
    Dim cat As ADOX.Catalog  
    Dim usrNew As ADOX.User  
    Dim usrLoop As ADOX.User  
    Dim grpLoop As ADOX.Group  
  
    Set cat = New ADOX.Catalog  
  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';" & _  
        "jet oledb:system database=" & _  
        "'system.mdw'"  
  
    With cat  
        'Create and append new group with a string.  
        .Groups.Append "Accounting"  
  
        ' Create and append new user with an object.  
        Set usrNew = New ADOX.User  
        usrNew.Name = "Pat Smith"  
        usrNew.ChangePassword "", "Password1"  
        .Users.Append usrNew  
  
        ' Make the user Pat Smith a member of the  
        ' Accounting group by creating and adding the  
        ' appropriate Group object to the user's Groups  
        ' collection. The same is accomplished if a User  
        ' object representing Pat Smith is created and  
        ' appended to the Accounting group Users collection  
        usrNew.Groups.Append "Accounting"  
  
        ' Enumerate all User objects in the  
        ' catalog's Users collection.  
        For Each usrLoop In .Users  
            Debug.Print "  " & usrLoop.Name  
            Debug.Print "    Belongs to these groups:"  
            ' Enumerate all Group objects in each User  
            ' object's Groups collection.  
            If usrLoop.Groups.Count <> 0 Then  
                For Each grpLoop In usrLoop.Groups  
                    Debug.Print "    " & grpLoop.Name  
                Next grpLoop  
            Else  
                Debug.Print "    [None]"  
            End If  
        Next usrLoop  
  
        ' Enumerate all Group objects in the default  
        ' workspace's Groups collection.  
        For Each grpLoop In .Groups  
            Debug.Print "  " & grpLoop.Name  
            Debug.Print "    Has as its members:"  
            ' Enumerate all User objects in each Group  
            ' object's Users collection.  
            If grpLoop.Users.Count <> 0 Then  
                For Each usrLoop In grpLoop.Users  
                    Debug.Print "    " & usrLoop.Name  
                Next usrLoop  
            Else  
                Debug.Print "    [None]"  
            End If  
        Next grpLoop  
  
        ' Delete new User and Group objects because this  
        ' is only a demonstration.  
        ' These two line are commented out because the sub "OwnersX" uses  
        ' the group "Accounting".  
'        .Users.Delete "Pat Smith"  
'        .Groups.Delete "Accounting"  
  
    End With  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set usrNew = Nothing  
    Exit Sub  
  
GroupXError:  
  
    Set cat = Nothing  
    Set usrNew = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndGroupVB  
```  
  
## <a name="see-also"></a>Consulte também  
 [(Grupos de ADOX) do método append](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Acrescente o método (ADOX usuários)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Objeto de catálogo (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Método ChangePassword (ADOX)](../../../ado/reference/adox-api/changepassword-method-adox.md)   
 [Objeto de grupo (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)   
 [Coleção de grupos (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Objeto de usuário (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)   
 [Coleção Users (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
