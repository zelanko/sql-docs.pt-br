---
title: Adicionando vários campos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb62318b9f8eb03fbd3c9732dc8ad0caa9127d17
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63294420"
---
# <a name="adding-multiple-fields-and-values"></a>Adicionando vários campos e valores
Ocasionalmente, talvez seja mais eficiente para passar uma matriz de campos e seus valores correspondentes para o **AddNew** método, em vez de configuração **valor** várias vezes para cada novo campo. Se *FieldList* é uma matriz *valores* também deve ser uma matriz com o mesmo número de membros; caso contrário, ocorrerá um erro. A ordem dos nomes de campo deve corresponder à ordem dos valores de campo em cada matriz. O código a seguir passa uma matriz de campos e uma matriz de valores para o **AddNew** método.

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
