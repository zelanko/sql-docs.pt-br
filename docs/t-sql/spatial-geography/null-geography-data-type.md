---
title: NULL (tipo de dados geography) | Microsoft Docs
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
- Null (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Null (geography Data Type)
- Null method
ms.assetid: bb464b06-86e0-4b8b-ad78-04bd33b6069c
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 48df84157bf4b54c45c734cdc9338a95fc1b13ab
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="null-geography-data-type"></a>Null (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Uma propriedade somente leitura que fornece uma instância nula da **geografia** tipo.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Null  
```  
  
## <a name="arguments"></a>Argumentos  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo: **geografia**  
  
 Tipo CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentários  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir recupera uma instância nula de `geography`.  
  
```  
DECLARE @g geography;   
SET @g = geography::[Null];  
SELECT @g  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos de Geografia estática estendidos](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  

