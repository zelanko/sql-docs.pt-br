---
title: Informações de erro relacionada ao conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
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
ms.openlocfilehash: 2dab1996d2915757ba6e7834b5e41bd6eade41c6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="recordset-related-error-information"></a>Informações de erro relacionada ao conjunto de registros
Durante o processamento em lotes, o **Status** propriedade do **registros** objeto fornece informações sobre os registros individuais no **registros**. Antes de uma atualização do lote ocorre, o **Status** propriedade o **registros** reflete as informações sobre os registros adicionados, alterados e excluídos. Depois de **UpdateBatch** foi chamado, o **Status** propriedade indica o êxito ou falha da operação. Você move de um registro para o **registros**, o valor da **Status** alterações de propriedade para descrever o status do registro atual.
