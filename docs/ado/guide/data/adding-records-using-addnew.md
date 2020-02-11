---
title: Adicionando registros usando AddNew | Microsoft Docs
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
- editing data [ADO], AddNew method
ms.assetid: cab4adff-f22f-4fb1-9217-f8138c795268
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 36f6bad9a8f0d74a81d02ce64c78d7a91ddc0fa8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926289"
---
# <a name="adding-records-using-addnew-method"></a>Adicionando registros usando o método AddNew
Esta é a sintaxe básica do método **AddNew** :

 *conjunto de registros*. *FieldList*de AddNew, *valores*

 Os argumentos *FieldList* e *Values* são opcionais. *FieldList* é um único nome ou uma matriz de nomes ou posições ordinais dos campos no novo registro.

 O argumento *Values* é um único valor ou uma matriz de valores para os campos no novo registro.

 Normalmente, quando você pretende adicionar um único registro, você chamará o método **AddNew** sem nenhum argumento. Especificamente, você chamará **AddNew**; definir o **valor** de cada campo no novo registro; em seguida, chame **Update** ou **UpdateBatch**, ou ambos. Você pode certificar-se de que o **conjunto de registros** dá suporte à adição de novos registros usando a propriedade de **suporte** com a constante enumerada **adAddNew** .

 O código a seguir usa essa técnica para adicionar um novo transportador ao **conjunto de registros**de exemplo. SQL Server fornece automaticamente o valor do campo transportadora. Portanto, o código não tenta fornecer um valor de campo para os novos registros.

```
'BeginAddNew1.1
If objRs.Supports(adAddNew) Then
    With objRs
        .AddNew
        .Fields("CompanyName") = "Sample Shipper"
        .Fields("Phone") = "(931) 555-6334"
        .Update
    End With
End If
'EndAddNew1.1
```

## <a name="remarks"></a>Comentários
 Como esse código usa um **conjunto de registros** desconectado com um cursor do lado do cliente no modo de lote, você deve reconectar o **conjunto de registros** à fonte de dados com um novo objeto de **conexão** antes de poder chamar o método **UpdateBatch** para postar alterações no banco de dado. Isso é feito facilmente usando a nova função **GetNewConnection**.
