---
title: 'Instanciação de evento ADO: Visual Basic | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
ms.assetid: dce0a2a3-326f-4aaf-a822-6c5549833afa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0223d4d4346f26ff9339fce3cbc43be9bfcbe82
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772474"
---
# <a name="ado-event-instantiation-visual-basic"></a>Instanciação de evento ADO: Visual Basic
Para tratar eventos ADO no Microsoft® Visual Basic®, você deve declarar uma variável de nível de módulo usando o **WithEvents** palavra-chave. A variável pode ser declarada somente como parte de um módulo de classe e deve ser declarada no nível de módulo. Isso não é tão restritivo quanto parece, no entanto, como Visual Basic **formulário** objetos também são classes. A maneira mais simples para lidar com eventos ADO é declarar uma variável usando **WithEvents**. A exemplo a seguir identifica os **eventos ConnectComplete** evento para um **Conexão** objeto:  
  
```  
' BeginEventExampleVB02  
Dim WithEvents connEvent As Connection  
Attribute connEvent.VB_VarHelpID = -1  
  
Private Sub Form_Load()  
Dim strConn As String  
  
   ' Create a new object with event  
   ' handling enabled.  
   strConn = "Provider=sqloledb;" & _  
      "Data Source=MyServer;" & _  
      "Initial Catalog=Northwind;" & _  
      "Integrated Security=SSPI;"  
   Set connEvent = New ADODB.Connection  
   connEvent.Open strConn  
End Sub  
  
Private Sub connEvent_ConnectComplete(ByVal pError As ADODB.Error, _  
    adStatus As ADODB.EventStatusEnum, _  
    ByVal pConnection As ADODB.Connection)  
Dim strMsg As String  
  
   If adStatus = adStatusErrorsOccurred Then  
      Select Case pError.Number  
         Case adErrOperationCancelled  
            ' The operation was cancelled in the  
            ' Will event. Notify the user and exit.  
            strMsg = "I'm sorry you can't connect right now." & vbCrLf  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
         Case Else  
            strMsg = "Error " & Format(pError.Number) & vbCrLf  
            strMsg = strMsg & pError.Description  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
      End Select  
   End If  
   frmWait.btnOK.Enabled = True  
End Sub  
' EndEventExampleVB02  
```  
  
 O **Conexão** objeto é declarado na **formulário** nível usando o **WithEvents** palavra-chave para habilitar a manipulação de eventos. O manipulador de eventos Form_Load efetivamente cria o objeto, atribuindo um novo **Conexão** objeto *connEvent* e, em seguida, abre a conexão. Obviamente, um aplicativo real faria mais processamento no manipulador de eventos Form_Load que foi mostrado aqui.
