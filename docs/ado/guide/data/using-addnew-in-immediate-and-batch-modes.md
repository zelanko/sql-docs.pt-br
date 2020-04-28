---
title: Usando AddNew nos modos Immediate e Batch | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, editing data
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: ed314bb9-e188-4658-a68c-a2abc49610be
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 265b1dcd3cdc1aa7f18f0ca54dc2cf54df2da158
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923622"
---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>Usar AddNew em modos de lote e imediatos
O comportamento do método **AddNew** depende do modo de atualização do objeto **Recordset** e se você passa os argumentos *FieldList* e *Values* .  
  
 No modo de atualização imediata (no qual o provedor grava as alterações na fonte de dados subjacente quando você chama o método **Update** ), chamar o método **AddNew** sem argumentos define a propriedade **EditMode** como **adEditAdd.** O provedor armazena em cache qualquer valor de campo alterado localmente. Chamar o método **Update** posta o novo registro no banco de dados e redefine a propriedade **EditMode** como **adEditNone.** Se você passar os argumentos *FieldList* e *Values* , o ADO imediatamente posta o novo registro no banco de dados (nenhuma chamada de **atualização** é necessária); o valor da propriedade **EditMode** não é alterado (**adEditNone**).  
  
 No modo de atualização do lote, chamar o método **AddNew** sem argumentos define a propriedade **EditMode** como **adEditAdd**. O provedor armazena em cache qualquer valor de campo alterado localmente. Chamar o método **Update** adiciona o novo registro ao conjunto de **registros** atual e redefine a propriedade **EditMode** como **adEditNone**, mas o provedor não publica as alterações no banco de dados subjacente até que você chame o método **UpdateBatch** . Se você passar os argumentos *FieldList* e *Values* , o ADO enviará o novo registro ao provedor para armazenamento em um cache; Você precisa chamar o método **UpdateBatch** para postar o novo registro no banco de dados subjacente. Para obter mais informações sobre **Update** e **UpdateBatch**, consulte [atualizando e persistindo dados](../../../ado/guide/data/updating-and-persisting-data.md).
