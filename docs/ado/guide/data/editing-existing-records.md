---
title: Editando registros existentes | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], existing records
ms.assetid: 17ce1263-5897-452a-9ea5-c7f96b33df65
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6bd1e02bf406906cc8a893ccee66a408b38510f3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702068"
---
# <a name="editing-existing-records"></a>Editar registros existentes
Para editar os registros existentes, mova para a linha que você deseja editar e alterar o **valor** propriedade dos campos que você deseja alterar. Para obter mais informações sobre o **campo** do objeto **valor** propriedade, consulte [examinando dados](../../../ado/guide/data/examining-data.md). Dependendo do seu tipo de cursor, você usará **atualização** ou **UpdateBatch** para enviar alterações de volta para a fonte de dados. Para obter mais informações, consulte [Updating e persistência de dados](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 É geralmente mais eficiente usar um procedimento armazenado com um objeto de comando para executar atualizações, bem como para executar outras operações, como um procedimento armazenado não exige a criação de um cursor. Para obter mais informações sobre cursores, consulte [Noções básicas sobre cursores e bloqueios](../../../ado/guide/data/understanding-cursors-and-locks.md).
