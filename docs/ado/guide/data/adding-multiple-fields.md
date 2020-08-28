---
description: Adicionando vários campos e valores
title: Adicionando vários campos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], adding multiple fields
- editing data [ADO], AddNew method
ms.assetid: f3648ef4-9f36-4991-a868-83a617389844
author: rothja
ms.author: jroth
ms.openlocfilehash: c661e8e99ae9651a4b89f8facad238d5f83564e9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991767"
---
# <a name="adding-multiple-fields-and-values"></a>Adicionando vários campos e valores
Ocasionalmente, pode ser mais eficiente passar uma matriz de campos e seus valores correspondentes para o método **AddNew** , em vez de definir **Value** várias vezes para cada novo campo. Se *FieldList* for uma matriz, *os valores* também deverão ser uma matriz com o mesmo número de membros; caso contrário, ocorrerá um erro. A ordem dos nomes de campo deve corresponder à ordem dos valores de campo em cada matriz. O código a seguir passa uma matriz de campos e uma matriz de valores para o método **AddNew** .

```
'BeginAddNew2
    Dim avarFldNames As Variant
    Dim avarFldValues As Variant

    avarFldNames = Array("CompanyName", "Phone")
    avarFldValues = Array("Sample Shipper 2", "(931) 555-6334")

    If objRs1.Supports(adAddNew) Then
        objRs1.AddNew avarFldNames, avarFldValues
    End If

    'Re-establish a Connection and update
    Set objRs1.ActiveConnection = GetNewConnection
    objRs1.UpdateBatch
'EndAddNew2
```
