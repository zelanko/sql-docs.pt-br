---
description: Erros (ADO)
title: Erros (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 392d1f2fdfc0a7fe2e0cf9e1e14efb77f396acfd
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806130"
---
# <a name="errors-ado"></a>Erros (ADO)
Qualquer operação que envolva objetos ADO pode gerar um ou mais erros de provedor. À medida que cada erro ocorre, um ou mais objetos de **erro** são colocados na coleção de **erros** do objeto de **conexão** . Para obter detalhes sobre como tratar avisos e erros em seu aplicativo ADO, consulte [tratamento de erros](./error-handling.md).  
  
 Erros de aplicativo podem ser gerados por um mecanismo separado. Por exemplo, em Visual Basic, o objeto **Err** conterá erros no nível do aplicativo.