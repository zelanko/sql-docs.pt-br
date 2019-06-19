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
manager: jroth
ms.openlocfilehash: ef5f6cc4a262cecc81a8dd72f2d3e3f6a7e2fded
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700415"
---
# <a name="recordset-related-error-information"></a>Informações de erro relacionadas ao conjunto de registros
Durante o processamento em lotes, o **Status** propriedade da **conjunto de registros** objeto fornece informações sobre os registros individuais no **conjunto de registros**. Antes que uma atualização em lotes ocorra, o **Status** propriedade da **Recordset** reflete as informações sobre os registros sejam adicionados, alterados e excluídos. Após **UpdateBatch** tiver sido chamado, o **Status** propriedade indica o êxito ou falha da operação. Conforme você de registro em registro a **conjunto de registros**, o valor da **Status** alterações de propriedade para descrever o status do registro atual.
