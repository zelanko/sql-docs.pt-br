---
title: Edição de registros existentes | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], existing records
ms.assetid: 17ce1263-5897-452a-9ea5-c7f96b33df65
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08c6fbd16d40f0fa78cbb94f7f33094e839733d8
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270475"
---
# <a name="editing-existing-records"></a>Editar os registros existentes
Para editar os registros existentes, mova para a linha que você deseja editar e alterar o **valor** propriedade dos campos que você deseja alterar. Para obter mais informações sobre o **campo** do objeto **valor** propriedade, consulte [examinando dados](../../../ado/guide/data/examining-data.md). Dependendo de seu tipo de cursor, você usará **atualização** ou **UpdateBatch** para enviar as alterações de volta para a fonte de dados. Para obter mais informações, consulte [atualizando e persistir dados](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 É geralmente mais eficiente usar um procedimento armazenado com um objeto de comando para executar atualizações, bem como para executar outras operações, como um procedimento armazenado não exige a criação de um cursor. Para obter mais informações sobre cursores, consulte [Noções básicas sobre cursores e bloqueios](../../../ado/guide/data/understanding-cursors-and-locks.md).
