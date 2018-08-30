---
title: Indicadores | Microsoft Docs
description: Indicadores no OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bookmarks [OLE DB]
- OLE DB Driver for SQL Server, bookmarks
- rowsets [OLE DB], bookmarks
- OLE DB rowsets, bookmarks
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: b4f076bb22728aef50fd0a356c4c7e472585cfc5
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43033835"
---
# <a name="bookmarks"></a>Indicadores
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Os indicadores permitem que os consumidores voltem rapidamente para uma linha. Com os indicadores, os consumidores podem acessar linhas aleatoriamente com base no valor do indicador. A coluna do indicador é a coluna 0 no conjunto de linhas. O consumidor define o valor de campo dwFrag da estrutura associada como DBCOLUMNSINFO_ISBOOKMARK para indicar que a coluna é usada como um indicador. O consumidor também define a propriedade DBPROP_BOOKMARKS do conjunto de linhas como VARIANT_TRUE. Isso permite que a coluna 0 esteja presente no conjunto de linhas. Em seguida, o método **IRowsetLocate::GetRowsAt** é usado para buscar linhas, começando com a linha especificada como um deslocamento de um indicador.  
  
## <a name="see-also"></a>Consulte Também  
 [Conjuntos de linhas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
