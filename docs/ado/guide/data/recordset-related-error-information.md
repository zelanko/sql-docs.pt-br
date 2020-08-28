---
description: Informações de erro relacionadas ao conjunto de registros
title: Informações de erro relacionadas ao conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 454c62b969ee69e6186792ce77873c8c8fbb5704
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979807"
---
# <a name="recordset-related-error-information"></a>Informações de erro relacionadas ao conjunto de registros
Durante o processamento em lotes, a propriedade **status** do objeto **Recordset** fornece informações sobre os registros individuais no **conjunto de registros**. Antes que uma atualização do lote ocorra, a propriedade **status** do **conjunto de registros** reflete informações sobre os registros a serem adicionados, alterados e excluídos. Depois que **UpdateBatch** tiver sido chamado, a propriedade **status** indicará o êxito ou a falha da operação. À medida que você passa do registro para o registro no **conjunto de registros**, o valor da propriedade **status** é alterado para descrever o status do registro atual.
