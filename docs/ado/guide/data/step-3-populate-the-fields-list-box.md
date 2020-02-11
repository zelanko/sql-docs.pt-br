---
title: 'Etapa 3: preencher a caixa de listagem de campos | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 315c32dc-aeb1-4629-b30e-87b44e8f84d1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d7f351b90030e755dde8ad13905ef4533eff08e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924057"
---
# <a name="step-3-populate-the-fields-list-box"></a>Etapa 3: Preencher a caixa de listagem de campos
Para preencher a caixa de listagem campos, insira o seguinte código no manipulador de eventos de `lstMain`clique de:  
  
```  
Private Sub lstMain_Click()  
    Dim rec As Record  
    Dim rs As Recordset  
    Set rec = New Record  
    Set rs = New Recordset  
    grs.MoveFirst  
    grs.Move lstMain.ListIndex  
    lstDetails.Clear  
    rec.Open grs  
    Select Case rec.RecordType  
        Case adCollectionRecord:  
            Set rs = rec.GetChildren  
            While Not rs.EOF  
                lstDetails.AddItem rs(0)  
                rs.MoveNext  
            Wend  
        Case adSimpleRecord:  
            recFields rec, lstDetails, txtDetails  
  
        Case adStructDoc:  
    End Select  
  
End Sub  
```  
  
 Esse código declara e instancia os objetos `rec` Registro local e conjunto de registros e `rs`, respectivamente.  
  
 A linha correspondente ao recurso selecionado em `lstMain` torna-se a linha atual de `grs`. Em seguida, a caixa de listagem detalhes `rec` é desmarcada e aberta com `grs` a linha atual de como a origem.  
  
 Se o recurso for um registro de coleção, conforme especificado por [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md), o conjunto `rs` de registros local será aberto nos filhos de rec. Em `lstDetails` seguida, é preenchido com os valores das linhas `rs`de.  
  
 Se o recurso for um registro simples, `recFields` será chamado. Para obter mais informações `recFields`sobre o, consulte a próxima etapa.  
  
 Nenhum código será implementado se o recurso for um documento estruturado.  
  
## <a name="see-also"></a>Consulte Também  
 [Cenário de publicação na Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Etapa 2: inicializar a caixa de listagem principal](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [Etapa 4: Preencher a caixa de texto de detalhes](../../../ado/guide/data/step-4-populate-the-details-text-box.md)
