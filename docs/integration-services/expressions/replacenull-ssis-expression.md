---
title: REPLACENULL (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 70db7832-b5a0-4db5-a8ad-42ad8630d8e8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 335ccdfb3857ba7d32147424a46f76bc0ccdbe17
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71288429"
---
# <a name="replacenull-ssis-expression"></a>REPLACENULL (Expressão SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Retornará o valor do parâmetro da segunda expressão se o valor do parâmetro da primeira expressão for NULL; caso contrário, retornará o valor da primeira expressão.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
REPLACENULL(expression 1,expression 2)  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão 1*  
 O resultado desta expressão é verificado em relação a NULL.  
  
 *expressão 2*  
 O resultado desta expressão será retornado se a primeira expressão avaliar como NULL.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Comentários  
  
-   O comprimento de *expression 2* pode ser zero.  
  
-   REPLACENULL retornará um resultado nulo se qualquer argumento for nulo.  
  
-   Não há suporte para colunas de BLOB (DT_TEXT, DT_NTEXT, DT_IMAGE) para nenhum parâmetro.  
  
-   É esperado que as duas expressões tenham o mesmo tipo de retorno. Se isso não ocorrer, a função tentará converter a 2ª expressão para o tipo de retorno da 1ª, que pode resultar em erro se os tipos de dados forem incompatíveis.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 O exemplo a seguir substitui os valores nulos em uma coluna de banco de dados por uma cadeia de caracteres (1900-01-01). Esta função é usada principalmente em padrões comuns de Coluna derivada onde você deseja substituir os valores NULL por qualquer outra coisa.  
  
```  
REPLACENULL(MyColumn, "1900-01-01")  
```  
  
> [!NOTE]
>  O exemplo a seguir mostra como isso foi feito no [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]/ [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)].  
  
```  
(DT_DBTIMESTAMP) (ISNULL(MyColumn) ? "1900-01-01" : MyColumn)   
```  
  
  
