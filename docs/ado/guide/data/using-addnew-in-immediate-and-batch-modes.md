---
title: Usando AddNew em imediata e modos de lote | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 6295e4499a6f6f25f9111497012f2e9f1d6dc421
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47616644"
---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>Usar AddNew em modos de lote e imediatos
O comportamento do **AddNew** método depende do modo de atualização a **conjunto de registros** objeto e se você passa o *FieldList* e *valores*argumentos.  
  
 No modo de atualização imediata (no qual o provedor grava as alterações à fonte de dados subjacente depois de chamar o **atualize** método), chamar o **AddNew** método sem argumentos define o  **EditMode** propriedade para **adEditAdd.** O provedor armazena em cache localmente as alterações de valor de campo. Chamar o **atualização** método posta o novo registro ao banco de dados e redefine o **EditMode** propriedade **adEditNone.** Se você passar o *FieldList* e *valores* argumentos, o ADO posta imediatamente o novo registro ao banco de dados (sem **atualização** chamada é necessária); o **EditMode**  não altera o valor da propriedade (**adEditNone**).  
  
 No modo de atualização de lote, chamar o **AddNew** método sem argumentos define o **EditMode** propriedade a ser **adEditAdd**. O provedor armazena em cache localmente as alterações de valor de campo. Chamar o **atualização** método adiciona o novo registro atual **conjunto de registros** e redefine o **EditMode** propriedade **adEditNone**, mas o provedor não postam as alterações no banco de dados subjacente até que você chame o **UpdateBatch** método. Se você passar o *FieldList* e *valores* argumentos, ADO envia o novo registro para o provedor de armazenamento em um cache; você precisa chamar o **UpdateBatch** método para lançar o novo Registre-se ao banco de dados subjacente. Para obter mais informações sobre **atualização** e **UpdateBatch**, consulte [atualizando e persistência de dados](../../../ado/guide/data/updating-and-persisting-data.md).
