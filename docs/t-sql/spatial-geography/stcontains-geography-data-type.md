---
description: STContains (tipo de dados geography)
title: STContains (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STContains method (geography)
ms.assetid: b10e8f0a-2926-449a-82ea-be42543420ca
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: d3e9b03eac0107792b9b0cdb59359f5ad70b5474
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88459068"
---
# <a name="stcontains--geography-data-type"></a>STContains (tipo de dados geography)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  Especifica se a instância de **geography** de chamada contém espacialmente a instância de **geography** passada para o método.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STContains ( other_geography )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *other_geography*  
 É outra instância de **geography** a ser comparada com a instância na qual `STContains()` é invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de retorno do CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentários  
 Retorna 1 se a instância de **geography** de chamada contém espacialmente a instância de **geography** passada ao método; caso contrário, retorna 0. Retorna **null** se o SRID das duas instâncias de **geography** não são iguais.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STContains()` para testar duas instâncias de `geography` a fim de verificar se a primeira instância contém a segunda.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::Parse('CURVEPOLYGON (COMPOUNDCURVE (CIRCULARSTRING (-122.200928 47.454094, -122.810669 47.00648, -122.942505 46.687131, -121.14624 45.786679, -119.119263 46.183634), (-119.119263 46.183634, -119.273071 47.107523, -120.640869 47.569114, -122.200928 47.454094)))');  
SET @h = geography::Parse('POINT(-121.703796 46.893985)');  
```  
  
 `SELECT @g.STContains(@h);`  
  
  
