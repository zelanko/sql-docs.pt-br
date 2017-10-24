---
title: "Informações de erro relacionada ao conjunto de registros | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 279fcc0564f433234cbac730465e2af06a7eb5e7
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="recordset-related-error-information"></a>Informações de erro relacionada ao conjunto de registros
Durante o processamento em lotes, o **Status** propriedade do **registros** objeto fornece informações sobre os registros individuais no **registros**. Antes de uma atualização do lote ocorre, o **Status** propriedade o **registros** reflete as informações sobre os registros adicionados, alterados e excluídos. Depois de **UpdateBatch** foi chamado, o **Status** propriedade indica o êxito ou falha da operação. Você move de um registro para o **registros**, o valor da **Status** alterações de propriedade para descrever o status do registro atual.

