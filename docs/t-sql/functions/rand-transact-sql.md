---
title: RAND (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- RAND
- RAND_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RAND function
- values [SQL Server], random float
- random float value
ms.assetid: 363c84d6-b9fa-49ba-9a75-e44f27535ff6
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 8e7217f3acbd09c6986a7c60e96db522fdacf0f4
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39452083"
---
# <a name="rand-transact-sql"></a>RAND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Retorna um valor **float** pseudoaleatório de 0 a 1, exclusivo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RAND ( [ seed ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *seed*  
 É um número inteiro [expressão](../../t-sql/language-elements/expressions-transact-sql.md) (**tinyint**, **smallint** ou **int**) que fornece o valor de semente. Se *seed* não estiver especificado, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] atribuirá um valor de semente aleatório. Para um valor de semente especificado, o resultado retornado é sempre o mesmo.  
  
## <a name="return-types"></a>Tipos de retorno  
 **float**  
  
## <a name="remarks"></a>Remarks  
 Chamadas repetitivas de RAND() com o mesmo valor de semente retornam os mesmos resultados.  
  
 Para uma conexão, se RAND() for chamada com uma valor de semente especificado, todas as chamadas subsequentes de RAND() produzirão resultados com base na chamada de RAND() propagada. Por exemplo, a consulta a seguir sempre retornará a mesma sequência de números.  
  
```  
SELECT RAND(100), RAND(), RAND()   
```  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir produz quatro números aleatórios diferentes que são gerados pela função RAND.  
  
```  
DECLARE @counter smallint;  
SET @counter = 1;  
WHILE @counter < 5  
   BEGIN  
      SELECT RAND() Random_Number  
      SET @counter = @counter + 1  
   END;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  
