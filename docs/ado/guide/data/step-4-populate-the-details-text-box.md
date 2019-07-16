---
title: 'Etapa 4: Preencha a caixa de texto de detalhes | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: cb4273e2-c907-4a86-a621-3bf110088228
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 90748ca7f725ddbf947d9686b846695da0c6626c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924063"
---
# <a name="step-4-populate-the-details-text-box"></a>Etapa 4: Preencher a caixa de texto de detalhes
Para preencher a caixa de texto de detalhes, criar uma nova sub-rotina denominada **recFields** e insira o seguinte código:  
  
```  
Sub recFields(r As Record, l As ListBox, t As TextBox)  
    Dim f As Field  
    Dim s As Stream  
    Set s = New Stream  
    Dim str As String  
  
    For Each f In r.Fields  
        l.AddItem f.Name & ": " & f.Value  
    Next  
    t.Text = ""  
    If r!RESOURCE_CONTENTCLASS = "text/plain" Then  
        s.Open r, adModeRead, adOpenStreamFromRecord  
        str = s.ReadText(1)  
        s.Position = 0  
        If Asc(Mid(str, 1, 1)) = 63 Then '//63 = "?"  
            s.Charset = "ascii"  
            s.Type = adTypeText  
        End If  
        t.Text = s.ReadText(adReadAll)  
    End If  
End Sub  
```  
  
 Esse código preenche `lstDetails` com os campos e valores do registro simple passado para `recFields`. Se o recurso for um arquivo de texto, um Stream de texto é aberto do registro de recurso. O código determina se o conjunto de caracteres ASCII e copia o conteúdo do Stream em `txtDetails`.  
  
## <a name="see-also"></a>Consulte também  
 [Cenário de publicação na Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Etapa 3: Preencha a caixa de lista de campos](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
