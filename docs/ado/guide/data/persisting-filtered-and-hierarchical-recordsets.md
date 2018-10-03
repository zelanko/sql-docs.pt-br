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
manager: craigg
ms.openlocfilehash: 53e28fdfbc49b53c4927bbcc0d5a6a8dc44b3d6d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811914"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>Persistência de conjunto de registros filtrados e hierárquicos
Se o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade está em vigor para o **conjunto de registros**, somente as linhas acessíveis sob o filtro são salvos. Se o **conjunto de registros** é hierárquico, o filho atual **conjunto de registros** e seus filhos são salvas, incluindo o pai **conjunto de registros**. Se o **salve** método de um filho **Recordset** é chamado, o filho e todos os seus filhos são salvas, mas o pai não é. Para obter mais informações sobre hierárquica **conjuntos de registros**, consulte [Data Shaping](../../../ado/guide/data/data-shaping.md).  
  
> [!NOTE]
>  Algumas limitações se aplicam ao salvar hierárquica **conjuntos de registros** (formas de dados) em formato XML. Para obter mais informações, consulte [manter registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).
