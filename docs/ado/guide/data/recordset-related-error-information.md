---
description: Informações de erro relacionadas ao conjunto de registros
title: Informações de erro relacionadas ao conjunto de registros | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7806d446c200f4d90ec458ceea268435ad9994e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452948"
---
# <a name="recordset-related-error-information"></a>Informações de erro relacionadas ao conjunto de registros
Durante o processamento em lotes, a propriedade **status** do objeto **Recordset** fornece informações sobre os registros individuais no **conjunto de registros**. Antes que uma atualização do lote ocorra, a propriedade **status** do **conjunto de registros** reflete informações sobre os registros a serem adicionados, alterados e excluídos. Depois que **UpdateBatch** tiver sido chamado, a propriedade **status** indicará o êxito ou a falha da operação. À medida que você passa do registro para o registro no **conjunto de registros**, o valor da propriedade **status** é alterado para descrever o status do registro atual.
