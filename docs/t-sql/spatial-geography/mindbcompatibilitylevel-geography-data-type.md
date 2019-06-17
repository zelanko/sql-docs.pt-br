---
title: MinDbCompatibilityLevel (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MinDbCompatibilityLevel
- MinDbCompatibilityLevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MinDbCompatibilityLevel method (geography)
ms.assetid: a9e44748-4a9e-4179-abc4-7631597be5a7
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 32d7df746e51612dd39360ff6702e9489111ce04
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65937255"
---
# <a name="mindbcompatibilitylevel-geography-data-type"></a>MinDbCompatibilityLevel (tipo de dados de geografia)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna a compatibilidade mínima de banco de dados que reconhece o tipo de dados **geography**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
. MinDbCompatibilityLevel ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de retorno do CLR: **int**  
  
## <a name="remarks"></a>Remarks  
 Use `MinDbCompatibilityLevel()` para testar a compatibilidade de um objeto espacial antes de alterar o nível de compatibilidade em um banco de dados. Um tipo de **geografia** inválido retorna 110.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [Compatibilidade com versões anteriores do Mecanismo de Banco de Dados do SQL Server](../../database-engine/sql-server-database-engine-backward-compatibility.md)  
  
  
