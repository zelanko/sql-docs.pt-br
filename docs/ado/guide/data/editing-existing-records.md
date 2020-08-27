---
description: Editar registros existentes
title: Editando registros existentes | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], existing records
ms.assetid: 17ce1263-5897-452a-9ea5-c7f96b33df65
author: rothja
ms.author: jroth
ms.openlocfilehash: 35c2376031e96a19c4a761a9826e47be2306518e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991327"
---
# <a name="editing-existing-records"></a>Editar registros existentes
Para editar os registros existentes, mova para a linha que você deseja editar e altere a propriedade **valor** dos campos que você deseja alterar. Para obter mais informações sobre a propriedade **Value** do objeto **Field** , consulte [examinando dados](./examining-data.md). Dependendo do tipo de cursor, você usará **Update** ou **UpdateBatch** para enviar as alterações de volta para a fonte de dados. Para obter mais informações, consulte [atualizando e persistindo dados](./updating-and-persisting-data.md).  
  
 Geralmente, é mais eficiente usar um procedimento armazenado com um objeto de comando para executar atualizações, bem como para executar outras operações, porque um procedimento armazenado não requer a criação de um cursor. Para obter mais informações sobre cursores, consulte [noções básicas sobre cursores e bloqueios](./understanding-cursors-and-locks.md).