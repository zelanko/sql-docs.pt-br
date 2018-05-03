---
title: Informações de erro relacionada ao conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 142177831126100343a293bb1467726dcd0e29e0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="recordset-related-error-information"></a>Informações de erro relacionada ao conjunto de registros
Durante o processamento em lotes, o **Status** propriedade do **registros** objeto fornece informações sobre os registros individuais no **registros**. Antes de uma atualização do lote ocorre, o **Status** propriedade o **registros** reflete as informações sobre os registros adicionados, alterados e excluídos. Depois de **UpdateBatch** foi chamado, o **Status** propriedade indica o êxito ou falha da operação. Você move de um registro para o **registros**, o valor da **Status** alterações de propriedade para descrever o status do registro atual.
