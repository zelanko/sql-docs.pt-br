---
title: "Conjuntos de registros filtrados e hierárquicos persistentes | Microsoft Docs"
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
- filtered Recordset persistence [ADO]
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: d01aeb4d-4e43-450b-b3f2-0c27eaaf9f86
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6d7ad27e3694b7a92e560170e699f62d76d5e6b0
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>Persistindo filtrados e conjuntos de registros hierárquicos
Se o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade está em vigor para o **registros**, somente as linhas acessíveis com o filtro serão salvas. Se o **Recordset** é hierárquico, o filho atual **registros** e seus filhos são salvos, incluindo o pai **registros**. Se o **salvar** método de um filho **registros** é chamado, o filho e todos os seus filhos são salvas, mas o pai não é. Para obter mais informações sobre hierárquica **conjuntos de registros**, consulte [modelagem de dados](../../../ado/guide/data/data-shaping.md).  
  
> [!NOTE]
>  Algumas limitações se aplicam ao salvar hierárquica **conjuntos de registros** (formas de dados) em formato XML. Para obter mais informações, consulte [manter registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).
