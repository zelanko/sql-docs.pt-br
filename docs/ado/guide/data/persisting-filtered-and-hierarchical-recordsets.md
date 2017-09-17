---
title: "Conjuntos de registros filtrados e hierárquicos persistentes | Microsoft Docs"
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
- filtered Recordset persistence [ADO]
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: d01aeb4d-4e43-450b-b3f2-0c27eaaf9f86
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8de12620e57fe9cf7235c2a1f5a1442b429197d0
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>Persistindo filtrados e conjuntos de registros hierárquicos
Se o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade está em vigor para o **registros**, somente as linhas acessíveis com o filtro serão salvas. Se o **Recordset** é hierárquico, o filho atual **registros** e seus filhos são salvos, incluindo o pai **registros**. Se o **salvar** método de um filho **registros** é chamado, o filho e todos os seus filhos são salvas, mas o pai não é. Para obter mais informações sobre hierárquica **conjuntos de registros**, consulte [modelagem de dados](../../../ado/guide/data/data-shaping.md).  
  
> [!NOTE]
>  Algumas limitações se aplicam ao salvar hierárquica **conjuntos de registros** (formas de dados) em formato XML. Para obter mais informações, consulte [manter registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).
