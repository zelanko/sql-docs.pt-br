---
title: MinDbCompatibilityLevel (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MinDbCompatibilityLevel
- MinDbCompatibilityLevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MinDbCompatibilityLevel method (geography)
ms.assetid: a9e44748-4a9e-4179-abc4-7631597be5a7
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6c95aafc0278834c6108b99dd67908958fb47b17
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="mindbcompatibilitylevel-geography-data-type"></a>MinDbCompatibilityLevel (tipo de dados de geografia)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna a compatibilidade de banco de dados mínimo que reconhece o **geografia** tipo de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
. MinDbCompatibilityLevel ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **int**  
  
 Tipo de retorno CLR: **int**  
  
## <a name="remarks"></a>Comentários  
 Use `MinDbCompatibilityLevel()` para testar a compatibilidade de um objeto espacial antes de alterar o nível de compatibilidade em um banco de dados. Inválido **geografia** digite retorna 110.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-testing-circularstring-type-for-compatibility-with-compatibility-level-110"></a>A. Testando a compatibilidade do tipo CircularString com o nível 110 de compatibilidade  
 O exemplo a seguir testa a compatibilidade de uma instância de `CircularString` com uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
DECLARE @g geometry = 'CIRCULARSTRING(-120.533 46.566, -118.283 46.1, -122.3 47.45)';  
IF @g.MinDbCompatibilityLevel() <= 110  
BEGIN  
    SELECT @g.ToString();  
END  
  
```  
  
### <a name="b-testing-linestring-type-for-compatibility-with-compatibility-level-100"></a>B. Testando a compatibilidade do tipo LineString com o nível 100 de compatibilidade  
 O exemplo a seguir testa a compatibilidade de uma instância de `LineString` com o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]:  
  
```  
DECLARE @g geometry = 'LINESTRING(-120.533 46.566, -118.283 46.1, -122.3 47.45)';  
IF @g.MinDbCompatibilityLevel() <= 100  
BEGIN  
    SELECT @g.ToString();  
END  
  
```  
  
### <a name="c-testing-the-value-of-a-geography-instance-for-compatibility"></a>C. Testando a compatibilidade do valor de uma instância de Geografia  
 O exemplo a seguir mostra os níveis de compatibilidade de duas instâncias `geography`. Um é menor do que um hemisfério e o outro é maior do que um hemisfério:  
  
```  
DECLARE @g geography = geography::Parse('POLYGON((0 -10, 120 -10, 240 -10, 0 -10))');  
DECLARE @h geography = geography::Parse('POLYGON((0 10, 120 10, 240 10, 0 10))');  
IF (@g.EnvelopeAngle() >= 90)  
BEGIN  
SELECT @g.MinDbCompatibilityLevel();  
END     
IF (@h.EnvelopeAngle() < 90)  
BEGIN  
SELECT @h.MinDbCompatibilityLevel();  
END  
  
```  
  
 A primeira instrução SELECT retorna 110 e a segunda instrução SELECT retorna 100.  
  
## <a name="see-also"></a>Consulte também  
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [Compatibilidade com versões anteriores do mecanismo de banco de dados SQL Server](../../database-engine/sql-server-database-engine-backward-compatibility.md)  
  
  

