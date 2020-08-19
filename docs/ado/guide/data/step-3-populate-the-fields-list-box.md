---
description: 'Etapa 3: Preencher a caixa de listagem de campos'
title: 'Etapa 3: preencher a caixa de listagem de campos | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 315c32dc-aeb1-4629-b30e-87b44e8f84d1
author: rothja
ms.author: jroth
ms.openlocfilehash: d3a7378cfdce29094f5ae4271b9fe7bff7516753
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452788"
---
# <a name="step-3-populate-the-fields-list-box"></a>Etapa 3: Preencher a caixa de listagem de campos
Para preencher a caixa de listagem campos, insira o seguinte código no manipulador de eventos de clique de `lstMain` :  
  
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
  
 Esse código declara e instancia os objetos Registro local e conjunto de registros `rec` e `rs` , respectivamente.  
  
 A linha correspondente ao recurso selecionado em `lstMain` torna-se a linha atual de `grs` . Em seguida, a caixa de listagem detalhes é desmarcada e `rec` aberta com a linha atual de `grs` como a origem.  
  
 Se o recurso for um registro de coleção, conforme especificado por [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md), o conjunto de registros local `rs` será aberto nos filhos de rec. Em seguida, `lstDetails` é preenchido com os valores das linhas de `rs` .  
  
 Se o recurso for um registro simples, `recFields` será chamado. Para obter mais informações sobre `recFields` o, consulte a próxima etapa.  
  
 Nenhum código será implementado se o recurso for um documento estruturado.  
  
## <a name="see-also"></a>Consulte Também  
 [Cenário de publicação na Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Etapa 2: inicializar a caixa de listagem principal](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [Etapa 4: Preencher a caixa de texto de detalhes](../../../ado/guide/data/step-4-populate-the-details-text-box.md)
