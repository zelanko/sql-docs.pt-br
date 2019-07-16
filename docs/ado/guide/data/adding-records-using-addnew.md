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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926289"
---
# <a name="adding-records-using-addnew-method"></a>Adicionando registros usando o método AddNew
Esta é a sintaxe básica do **AddNew** método:

 *conjunto de registros*. AddNew *FieldList*, *valores*

 O *FieldList* e *valores* argumentos são opcionais. *FieldList* é um único nome ou uma matriz de nomes ou as posições ordinais dos campos no novo registro.

 O *valores* argumento é um único valor ou uma matriz de valores para os campos no novo registro.

 Normalmente, quando você pretende adicionar um único registro, você chamará o **AddNew** método sem nenhum argumento. Especificamente, você chamará **AddNew**; defina as **valor** de cada campo no novo registro; e, em seguida, chame **atualização** ou **UpdateBatch**, ou ambos. Você pode garantir que seu **conjunto de registros** dá suporte à adição de novos registros usando o **dá suporte a** propriedade com o **adAddNew** constante enumerada.

 O código a seguir usa essa técnica para adicionar um novo remetente à amostra **conjunto de registros**. SQL Server fornece o valor do campo CódigoDaTransportadora automaticamente. Portanto, o código não tenta fornecer um valor de campo para os novos registros.

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
 Como esse código usa um desconectada **conjunto de registros** com um cursor do lado do cliente no modo de lote, você deve reconectar o **conjunto de registros** à fonte de dados com uma nova **Conexão** objeto antes de chamar o **UpdateBatch** método para lançar as alterações no banco de dados. Isso é feito facilmente usando a nova função **GetNewConnection**.
