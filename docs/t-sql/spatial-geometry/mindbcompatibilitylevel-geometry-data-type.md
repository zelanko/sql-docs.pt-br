---
title: MinDbCompatibilityLevel (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- MinDbCompatibilityLevel method (geometry)
ms.assetid: c848b974-8ccb-4c5c-a7eb-b019a9538d99
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ca5eacc943ff45cb8615f376a95a911355868541
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37971228"
---
# <a name="mindbcompatibilitylevel-geometry-data-type"></a>MinDbCompatibilityLevel (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna o nível mínimo de compatibilidade do banco de dados que reconhece a instância do tipo de dados de **geometry**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.MinDbCompatibilityLevel ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de retorno do CLR: **int**  
  
## <a name="remarks"></a>Remarks  
 Use `MinDbCompatibilityLevel()` para testar a compatibilidade de um objeto espacial antes de alterar o nível de compatibilidade em um banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-testing-circularstring-type-for-compatibility-with-compatibility-level-110"></a>A. Testando a compatibilidade do tipo CircularString com o nível 110 de compatibilidade  
 O exemplo a seguir testa a compatibilidade de uma instância de `CircularString` com uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(3 4, 8 9, 5 6)'; 
 IF @g.MinDbCompatibilityLevel() <= 110 
 BEGIN 
 SELECT @g.ToString(); 
 END
 ```  
  
### <a name="b-testing-linestring-type-for-compatibility-with-compatibility-level-100"></a>B. Testando a compatibilidade do tipo LineString com o nível 100 de compatibilidade  
 O exemplo a seguir testa a compatibilidade de uma instância de `LineString` com o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 9, 5 6)'; 
 IF @g.MinDbCompatibilityLevel() <= 100 
 BEGIN 
 SELECT @g.ToString(); 
 END
``` 
  
## <a name="see-also"></a>Consulte Também  
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  

