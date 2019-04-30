---
title: Informações de erro relacionados ao conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c4f13a77a9f03aa76fccc41a1fa19878dd935db0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187794"
---
# <a name="recordset-related-error-information"></a>Informações de erro relacionadas ao conjunto de registros
Durante o processamento em lotes, o **Status** propriedade da **conjunto de registros** objeto fornece informações sobre os registros individuais no **conjunto de registros**. Antes que uma atualização em lotes ocorra, o **Status** propriedade da **Recordset** reflete as informações sobre os registros sejam adicionados, alterados e excluídos. Após **UpdateBatch** tiver sido chamado, o **Status** propriedade indica o êxito ou falha da operação. Conforme você de registro em registro a **conjunto de registros**, o valor da **Status** alterações de propriedade para descrever o status do registro atual.
