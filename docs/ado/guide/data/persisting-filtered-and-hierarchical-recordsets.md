---
title: Conjuntos de registros filtrados e hierárquicos persistentes | Microsoft Docs
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
- filtered Recordset persistence [ADO]
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: d01aeb4d-4e43-450b-b3f2-0c27eaaf9f86
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d995e0d35f355f1d1b41fd0c6bcacd93da5b1b22
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>Persistindo filtrados e conjuntos de registros hierárquicos
Se o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade está em vigor para o **registros**, somente as linhas acessíveis com o filtro serão salvas. Se o **Recordset** é hierárquico, o filho atual **registros** e seus filhos são salvos, incluindo o pai **registros**. Se o **salvar** método de um filho **registros** é chamado, o filho e todos os seus filhos são salvas, mas o pai não é. Para obter mais informações sobre hierárquica **conjuntos de registros**, consulte [modelagem de dados](../../../ado/guide/data/data-shaping.md).  
  
> [!NOTE]
>  Algumas limitações se aplicam ao salvar hierárquica **conjuntos de registros** (formas de dados) em formato XML. Para obter mais informações, consulte [manter registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).
