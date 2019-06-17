---
title: SRIDs (Identificadores de Referência Espacial) | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: c1e96d37ae3d140eb2efddd6d3df5c656cc3afd7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013998"
---
# <a name="spatial-reference-identifiers-srids"></a>SRIDs (Spatial Reference Identifiers)
  Cada instância espacial tem um SRID (spatial reference identifier). O SRID corresponde a um sistema de referência espacial baseado no elipsoide específico usado para mapeamento de terra plana ou de terra redonda.  
  
> [!IMPORTANT]  
>  Para obter uma descrição detalhada e exemplos de recursos espaciais introduzidos no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], incluindo um novo SRID, baixe o white paper [Novos recursos espaciais no SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=226407).  
  
 Uma coluna espacial pode conter objetos com SRIDs diferentes. No entanto apenas instâncias espaciais com o mesmo SRID podem ser usadas ao executar operações com métodos de dados espaciais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em seus dados. O resultado de qualquer método espacial derivado de duas instâncias de dados espaciais será válido apenas se essas instâncias tiverem o mesmo SRID que é baseado na mesma unidade de medida, datum, e projeção usada para determinar as coordenadas das instâncias. As unidades mais comuns de medida de um SRID são metros ou metros quadrados.  
  
 Se duas instâncias espaciais não tiverem o mesmo SRID, os resultados de um método de Tipo de Dados `geometry` ou `geography` usado nas instâncias retornará NULL. Por exemplo, para que o seguinte termo de predicado retorne um resultado não NULL, as duas instâncias de `geometry`, `geometry1` e `geometry2`, devem ter o mesmo SRID:  
  
 `geometry1.STIntersects(geometry2) = 1`  
  
> [!NOTE]  
>  O sistema de identificação de referência espacial é definido pelo [padrão do EPSG (European Petroleum Survey Group)](https://go.microsoft.com/fwlink/?LinkId=99349) , que é um conjunto de padrões desenvolvido para armazenamento de dados geodésicos, de cartografia e de pesquisa. Esse padrão é de propriedade do Comitê de Pesquisa e Posicionamento da OGP (Oil and Gas Producers).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de tipos de dados espaciais](spatial-data-types-overview.md)  
  
  
