---
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
ms.openlocfilehash: cb51fa80cff0a17340e289886f0315ea167b88b0
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760952"
---
# <a name="recordset-related-error-information"></a>Informações de erro relacionadas ao conjunto de registros
Durante o processamento em lotes, a propriedade **status** do objeto **Recordset** fornece informações sobre os registros individuais no **conjunto de registros**. Antes que uma atualização do lote ocorra, a propriedade **status** do **conjunto de registros** reflete informações sobre os registros a serem adicionados, alterados e excluídos. Depois que **UpdateBatch** tiver sido chamado, a propriedade **status** indicará o êxito ou a falha da operação. À medida que você passa do registro para o registro no **conjunto de registros**, o valor da propriedade **status** é alterado para descrever o status do registro atual.
