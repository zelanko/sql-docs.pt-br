---
title: "Informações de erro relacionada ao conjunto de registros | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b1ad53c42fa3da686de10e3254c6fa7e3916d806
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="recordset-related-error-information"></a>Informações de erro relacionada ao conjunto de registros
Durante o processamento em lotes, o **Status** propriedade do **registros** objeto fornece informações sobre os registros individuais no **registros**. Antes de uma atualização do lote ocorre, o **Status** propriedade o **registros** reflete as informações sobre os registros adicionados, alterados e excluídos. Depois de **UpdateBatch** foi chamado, o **Status** propriedade indica o êxito ou falha da operação. Você move de um registro para o **registros**, o valor da **Status** alterações de propriedade para descrever o status do registro atual.
