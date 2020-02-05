---
title: Null (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Null (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Null (geography Data Type)
- Null method
ms.assetid: bb464b06-86e0-4b8b-ad78-04bd33b6069c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 775410c9a57d9bf030f34f84640522b766f0cf23
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68127375"
---
# <a name="null-geography-data-type"></a>Null (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Uma propriedade somente leitura que fornece uma instância nula do tipo de **geografia**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Null  
```  
  
## <a name="arguments"></a>Argumentos  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geografia**  
  
 Tipo do CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentários  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir recupera uma instância nula de `geography`.  
  
```  
DECLARE @g geography;   
SET @g = geography::[Null];  
SELECT @g  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Extended Static Geography Methods](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
