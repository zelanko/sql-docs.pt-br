---
title: GeomFromGML (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GeomFromGML_TSQL
- GeomFromGML
dev_langs:
- TSQL
helpviewer_keywords:
- GeomFromGML (geography Data Type)
- GeomFromGML method
ms.assetid: 470d0997-3cb0-4d34-9a45-b332fe432b14
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ec0d21afb92b000f29fb91c4e3b848b4881b99c7
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="geomfromgml-geography-data-type"></a>GeomFromGML (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Constrói um **geografia** instância dada uma representação no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] subconjunto do GML Geography Markup Language ().
  
Para obter mais informações sobre GML, consulte as seguintes especificações: [OGC Specifications, Geography Markup Language](http://go.microsoft.com/fwlink/?LinkId=93629)
  
Isso **geografia** método dá suporte ao tipo de dados **FullGlobe** instâncias ou a instâncias espaciais maiores que um hemisfério.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GeomFromGml ( GML_input, SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *GML_input*  
 É uma entrada XML a partir da qual o GML retornará um valor.  
  
 *SRID*  
 É um **int** SRID (ID) de fazer referência a expressão que representa o espaciais a **geografia** instância a ser retornada.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentários  
 Este método lança um **FormatException** se a entrada não for bem formatada.  
  
 Este método gerará **ArgumentException** se a entrada contiver uma borda oposta.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `GeomFromGml()` para criar uma instância `geography`.  
  
```  
DECLARE @g geography;  
DECLARE @x xml;  
SET @x = '<LineString xmlns="http://www.opengis.net/gml"><posList>47.656 -122.36 47.656 -122.343</posList></LineString>';  
SET @g = geography::GeomFromGml(@x, 4326);  
SELECT @g.ToString();  
```  
  
 O exemplo a seguir usa `GeomFromGml()` para criar uma instância `FullGlobe``geography`.  
  
```  
DECLARE @g geography;  
DECLARE @x xml;  
SET @x = '<FullGlobe xmlns="http://schemas.microsoft.com/sqlserver/2011/geography" />';  
SET @g = geography::GeomFromGml(@x, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos de Geografia estática estendidos](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  

