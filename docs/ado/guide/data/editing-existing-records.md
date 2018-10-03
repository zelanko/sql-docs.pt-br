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
manager: craigg
ms.openlocfilehash: 64262ae52b802398fc2060092a03e7469146f063
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692884"
---
# <a name="editing-existing-records"></a>Editar registros existentes
Para editar os registros existentes, mova para a linha que você deseja editar e alterar o **valor** propriedade dos campos que você deseja alterar. Para obter mais informações sobre o **campo** do objeto **valor** propriedade, consulte [examinando dados](../../../ado/guide/data/examining-data.md). Dependendo do seu tipo de cursor, você usará **atualização** ou **UpdateBatch** para enviar alterações de volta para a fonte de dados. Para obter mais informações, consulte [Updating e persistência de dados](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 É geralmente mais eficiente usar um procedimento armazenado com um objeto de comando para executar atualizações, bem como para executar outras operações, como um procedimento armazenado não exige a criação de um cursor. Para obter mais informações sobre cursores, consulte [Noções básicas sobre cursores e bloqueios](../../../ado/guide/data/understanding-cursors-and-locks.md).
