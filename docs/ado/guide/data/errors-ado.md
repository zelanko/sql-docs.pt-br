---
description: Erros (ADO)
title: Erros (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 8ae6611b-3069-4155-b014-c0c9da37be39
author: rothja
ms.author: jroth
ms.openlocfilehash: e779d6b0aac1e48f64d9544eda0c064f7278c496
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991307"
---
# <a name="errors-ado"></a>Erros (ADO)
Qualquer operação que envolva objetos ADO pode gerar um ou mais erros de provedor. À medida que cada erro ocorre, um ou mais objetos de **erro** são colocados na coleção de **erros** do objeto de **conexão** . Para obter detalhes sobre como tratar avisos e erros em seu aplicativo ADO, consulte [tratamento de erros](./error-handling.md).  
  
 Erros de aplicativo podem ser gerados por um mecanismo separado. Por exemplo, em Visual Basic, o objeto **Err** conterá erros no nível do aplicativo.