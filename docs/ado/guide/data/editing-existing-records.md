---
description: Editar registros existentes
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
ms.openlocfilehash: 3c720d43135cb54cd610ea6e9a7e32ac249c1081
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453448"
---
# <a name="editing-existing-records"></a>Editar registros existentes
Para editar os registros existentes, mova para a linha que você deseja editar e altere a propriedade **valor** dos campos que você deseja alterar. Para obter mais informações sobre a propriedade **Value** do objeto **Field** , consulte [examinando dados](../../../ado/guide/data/examining-data.md). Dependendo do tipo de cursor, você usará **Update** ou **UpdateBatch** para enviar as alterações de volta para a fonte de dados. Para obter mais informações, consulte [atualizando e persistindo dados](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Geralmente, é mais eficiente usar um procedimento armazenado com um objeto de comando para executar atualizações, bem como para executar outras operações, porque um procedimento armazenado não requer a criação de um cursor. Para obter mais informações sobre cursores, consulte [noções básicas sobre cursores e bloqueios](../../../ado/guide/data/understanding-cursors-and-locks.md).
