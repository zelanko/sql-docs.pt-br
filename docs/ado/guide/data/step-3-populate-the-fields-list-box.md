---
title: 'Etapa 3: Preencher a caixa de lista de campos | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 315c32dc-aeb1-4629-b30e-87b44e8f84d1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e88957f03b821ee350a575080bd4f0fd40ce466b
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272705"
---
# <a name="step-3-populate-the-fields-list-box"></a>Etapa 3: Preencher a caixa de lista de campos
Para preencher a caixa de lista de campos, insira o seguinte código para o manipulador de eventos de clique do `lstMain`:  
  
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
  
 Esse código declara e cria objetos locais de registro e o conjunto de registros, `rec` e `rs`, respectivamente.  
  
 A linha correspondente para o recurso selecionado no `lstMain` é feita a linha atual do `grs`. Em seguida, a caixa de lista de detalhes está desmarcada e `rec` é aberto com a linha atual do `grs` como a origem.  
  
 Se o recurso é um registro de coleção, conforme especificado por [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md), o conjunto de registros local `rs` é aberta nos filhos de rec. Em seguida, `lstDetails` é preenchida com os valores das linhas de `rs`.  
  
 Se o recurso de registro simple, `recFields` é chamado. Para obter mais informações sobre `recFields`, consulte a próxima etapa.  
  
 Nenhum código é implementado se o recurso for um documento estruturado.  
  
## <a name="see-also"></a>Consulte também  
 [Cenário de publicação na Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Etapa 2: Inicializar a caixa de listagem principal](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [Etapa 4: Preencher a caixa de texto de detalhes](../../../ado/guide/data/step-4-populate-the-details-text-box.md)
