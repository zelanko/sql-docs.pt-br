---
description: SRIDs (Spatial Reference Identifiers)
title: SRIDs (Identificadores de Referência Espacial) | Microsoft Docs
ms.date: 03/29/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Spatial Reference Identifiers (SRIDs)
- geodetic spatial data [SQL Server], identifiers
- SRID
ms.assetid: 0612658a-7d1b-4178-bdc2-42b914ea31a7
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2873242ab181ce3d550c5b4f2274fef368d5c0f8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473127"
---
# <a name="spatial-reference-identifiers-srids"></a>SRIDs (Spatial Reference Identifiers)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
  Cada instância espacial tem um SRID (spatial reference identifier). O SRID corresponde a um sistema de referência espacial baseado no elipsoide específico usado para mapeamento de terra plana ou de terra redonda.  
  
 Uma coluna espacial pode conter objetos com SRIDs diferentes. No entanto apenas instâncias espaciais com o mesmo SRID podem ser usadas ao executar operações com métodos de dados espaciais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em seus dados. O resultado de qualquer método espacial derivado de duas instâncias de dados espaciais será válido apenas se essas instâncias tiverem o mesmo SRID que é baseado na mesma unidade de medida, datum, e projeção usada para determinar as coordenadas das instâncias. As unidades mais comuns de medida de um SRID são metros ou metros quadrados.  
  
 Se duas instâncias espaciais não tiverem o mesmo SRID, os resultados de um método de Tipo de Dados **geometry** ou **geography** usado nas instâncias retornará NULL. Por exemplo, para que o seguinte termo de predicado retorne um resultado não NULL, as duas instâncias de **geometria** , `geometry1` e `geometry2`, devem ter o mesmo SRID:  
  
 `geometry1.STIntersects(geometry2) = 1`  
  
> [!NOTE]  
>  O sistema de identificação de referência espacial é definido pelo [padrão do EPSG (European Petroleum Survey Group)](https://go.microsoft.com/fwlink/?LinkId=99349) , que é um conjunto de padrões desenvolvido para armazenamento de dados geodésicos, de cartografia e de pesquisa. Esse padrão é de propriedade do Comitê de Pesquisa e Posicionamento da OGP (Oil and Gas Producers).  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral de tipos de dados espaciais](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
