---
title: "SRIDs (Identificadores de Referência Espacial) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Spatial Reference Identifiers (SRIDs)
- geodetic spatial data [SQL Server], identifiers
- SRID
ms.assetid: 0612658a-7d1b-4178-bdc2-42b914ea31a7
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 57420f270daa88e61add4810a7792ed6fdea8278
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="spatial-reference-identifiers-srids"></a>SRIDs (Spatial Reference Identifiers)
  Cada instância espacial tem um SRID (spatial reference identifier). O SRID corresponde a um sistema de referência espacial baseado no elipsoide específico usado para mapeamento de terra plana ou de terra redonda.  
  
> [!IMPORTANT]  
>  Para obter uma descrição detalhada e exemplos de recursos espaciais introduzidos no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], incluindo um novo SRID, baixe o white paper [Novos recursos espaciais no SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=226407).  
  
 Uma coluna espacial pode conter objetos com SRIDs diferentes. No entanto apenas instâncias espaciais com o mesmo SRID podem ser usadas ao executar operações com métodos de dados espaciais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em seus dados. O resultado de qualquer método espacial derivado de duas instâncias de dados espaciais será válido apenas se essas instâncias tiverem o mesmo SRID que é baseado na mesma unidade de medida, datum, e projeção usada para determinar as coordenadas das instâncias. As unidades mais comuns de medida de um SRID são metros ou metros quadrados.  
  
 Se duas instâncias espaciais não tiverem o mesmo SRID, os resultados de um método de Tipo de Dados **geometry** ou **geography** usado nas instâncias retornará NULL. Por exemplo, para que o seguinte termo de predicado retorne um resultado não NULL, as duas instâncias de **geometria** , `geometry1` e `geometry2`, devem ter o mesmo SRID:  
  
 `geometry1.STIntersects(geometry2) = 1`  
  
> [!NOTE]  
>  O sistema de identificação de referência espacial é definido pelo [padrão do EPSG (European Petroleum Survey Group)](http://go.microsoft.com/fwlink/?LinkId=99349) , que é um conjunto de padrões desenvolvido para armazenamento de dados geodésicos, de cartografia e de pesquisa. Esse padrão é de propriedade do Comitê de Pesquisa e Posicionamento da OGP (Oil and Gas Producers).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de tipos de dados espaciais](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  

