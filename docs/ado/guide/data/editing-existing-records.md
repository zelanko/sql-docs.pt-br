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
ms.openlocfilehash: ce8679c0c7b20dfaa641918f0447a2f77bfd474a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925431"
---
# <a name="editing-existing-records"></a>Editar registros existentes
Para editar os registros existentes, mova para a linha que você deseja editar e alterar o **valor** propriedade dos campos que você deseja alterar. Para obter mais informações sobre o **campo** do objeto **valor** propriedade, consulte [examinando dados](../../../ado/guide/data/examining-data.md). Dependendo do seu tipo de cursor, você usará **atualização** ou **UpdateBatch** para enviar alterações de volta para a fonte de dados. Para obter mais informações, consulte [Updating e persistência de dados](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 É geralmente mais eficiente usar um procedimento armazenado com um objeto de comando para executar atualizações, bem como para executar outras operações, como um procedimento armazenado não exige a criação de um cursor. Para obter mais informações sobre cursores, consulte [Noções básicas sobre cursores e bloqueios](../../../ado/guide/data/understanding-cursors-and-locks.md).
