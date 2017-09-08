---
title: MinDbCompatibilityLevel (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- MinDbCompatibilityLevel method (geometry)
ms.assetid: c848b974-8ccb-4c5c-a7eb-b019a9538d99
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 51bde32ba27af0ed46bb176ede7bb4a61ef15292
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="mindbcompatibilitylevel-geometry-data-type"></a>MinDbCompatibilityLevel (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna o nível de compatibilidade do banco de dados mínimo que reconhece o **geometria** instância de tipo de dados.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.MinDbCompatibilityLevel ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **int**  
  
 Tipo de retorno CLR: **int**  
  
## <a name="remarks"></a>Comentários  
 Use `MinDbCompatibilityLevel()` para testar a compatibilidade de um objeto espacial antes de alterar o nível de compatibilidade em um banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-testing-circularstring-type-for-compatibility-with-compatibility-level-110"></a>A. Testando a compatibilidade do tipo CircularString com o nível 110 de compatibilidade  
 O exemplo a seguir testa a compatibilidade de uma instância de `CircularString` com uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
 `DECLARE @g geometry = 'CIRCULARSTRING(3 4, 8 9, 5 6)';`  
  
 `IF @g.MinDbCompatibilityLevel() <= 110`  
  
 `BEGIN`  
  
 `SELECT @g.ToString();`  
  
 `END`  
  
### <a name="b-testing-linestring-type-for-compatibility-with-compatibility-level-100"></a>B. Testando a compatibilidade do tipo LineString com o nível 100 de compatibilidade  
 O exemplo a seguir testa a compatibilidade de uma instância de `LineString` com o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]:  
  
 `DECLARE @g geometry = 'LINESTRING(3 4, 8 9, 5 6)';`  
  
 `IF @g.MinDbCompatibilityLevel() <= 100`  
  
 `BEGIN`  
  
 `SELECT @g.ToString();`  
  
 `END`  
  
## <a name="see-also"></a>Consulte também  
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  


