---
title: Manter conjuntos de registros filtrados e hierárquicos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- filtered Recordset persistence [ADO]
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: d01aeb4d-4e43-450b-b3f2-0c27eaaf9f86
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cbd237580dc8c56284552e6fe2fb00e469832c5b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702050"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>Persistência de conjunto de registros filtrados e hierárquicos
Se o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade está em vigor para o **conjunto de registros**, somente as linhas acessíveis sob o filtro são salvos. Se o **conjunto de registros** é hierárquico, o filho atual **conjunto de registros** e seus filhos são salvas, incluindo o pai **conjunto de registros**. Se o **salve** método de um filho **Recordset** é chamado, o filho e todos os seus filhos são salvas, mas o pai não é. Para obter mais informações sobre hierárquica **conjuntos de registros**, consulte [Data Shaping](../../../ado/guide/data/data-shaping.md).  
  
> [!NOTE]
>  Algumas limitações se aplicam ao salvar hierárquica **conjuntos de registros** (formas de dados) em formato XML. Para obter mais informações, consulte [manter registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).
