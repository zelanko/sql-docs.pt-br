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
author: rothja
ms.author: jroth
ms.openlocfilehash: 71d8b825766ca94984ca2dc0b51577488178920f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761022"
---
# <a name="editing-existing-records"></a>Editar registros existentes
Para editar os registros existentes, mova para a linha que você deseja editar e altere a propriedade **valor** dos campos que você deseja alterar. Para obter mais informações sobre a propriedade **Value** do objeto **Field** , consulte [examinando dados](../../../ado/guide/data/examining-data.md). Dependendo do tipo de cursor, você usará **Update** ou **UpdateBatch** para enviar as alterações de volta para a fonte de dados. Para obter mais informações, consulte [atualizando e persistindo dados](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Geralmente, é mais eficiente usar um procedimento armazenado com um objeto de comando para executar atualizações, bem como para executar outras operações, porque um procedimento armazenado não requer a criação de um cursor. Para obter mais informações sobre cursores, consulte [noções básicas sobre cursores e bloqueios](../../../ado/guide/data/understanding-cursors-and-locks.md).
