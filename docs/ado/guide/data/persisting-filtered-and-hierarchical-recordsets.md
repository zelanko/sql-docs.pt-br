---
description: Persistência de conjunto de registros filtrados e hierárquicos
title: Persistência de conjuntos de registros filtrados e hierárquicos | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a69b491f4bb5834331b9cfa582b6f72d248ba317
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453058"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>Persistência de conjunto de registros filtrados e hierárquicos
Se a propriedade de [filtro](../../../ado/reference/ado-api/filter-property.md) estiver em vigor para o **conjunto de registros**, somente as linhas acessíveis no filtro serão salvas. Se o **conjunto de registros** for hierárquico, o **conjunto de registros** filho atual e seus filhos serão salvos, incluindo o **conjunto de registros**pai. Se o método **Save** de um **conjunto de registros** filho for chamado, o filho e todos os seus filhos serão salvos, mas o pai não será. Para obter mais informações sobre **conjuntos de registros**hierárquicos, consulte [Data Shaping](../../../ado/guide/data/data-shaping.md).  
  
> [!NOTE]
>  Algumas limitações se aplicam ao salvar **conjuntos de registros** hierárquicos (formas de dados) em formato XML. Para obter mais informações, consulte [persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).
