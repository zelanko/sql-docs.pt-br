---
title: REPLACE (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- replacing string expression
- REPLACE function
ms.assetid: a6837043-ea70-4c6a-9c7a-6868b02b2adc
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dabde936354e052a7a670b0235b994edf26093f3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178286"
---
# <a name="replace-ssis-expression"></a>REPLACE (Expressão SSIS)
  Retorna uma expressão de caractere depois de substituir uma cadeia de caracteres na expressão por uma cadeia diferente ou vazia.  
  
> [!NOTE]  
>  A função REPLACE geralmente usa cadeias de caracteres longos. As consequências do truncamento podem ser controladas muito bem ou causam um aviso ou um erro. Para obter mais informações, consulte [Sintaxe &#40;SSIS&#41;](syntax-ssis.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
REPLACE(character_expression,searchstring,replacementstring)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É uma expressão de caractere válida que a função pesquisa.  
  
 *searchstring*  
 É uma expressão de caractere válida que a função tenta localizar.  
  
 *replacementstring*  
 É uma expressão de caractere válida que é a expressão de substituição.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Comentários  
 O comprimento de *searchstring* não deve ser zero.  
  
 O comprimento de *replacementstring* pode ser zero.  
  
 Os argumentos *searchstring* e *replacementstring* podem usar variáveis e colunas.  
  
 REPLICATE funciona apenas com o tipo de dados DT_WSTR. Os argumentos*character_expression1, character_expression2,* e *character_expression3* , que são literais de cadeia de caracteres ou colunas de dados com o tipo de dados DT_STR, são implicitamente convertidos para o tipo de dados DT_WSTR antes de REPLACE executar sua operação. Outros tipos de dados devem ser explicitamente convertidos para o tipo de dados DT_WSTR. Para obter mais informações, consulte [Cast &#40;Expressão do SSIS&#41;](cast-ssis-expression.md).  
  
 REPLACE retornará um resultado nulo se qualquer argumento for nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo usa um literal de cadeia de caracteres. O resultado de retorno é “Toda Bicicleta de Terreno”.  
  
```  
REPLACE("Mountain Bike", "Mountain","All Terrain")  
```  
  
 Este exemplo remove a cadeia de caracteres "Bike" da coluna **Product** .  
  
```  
REPLACE(Product, "Bike","")  
```  
  
 Este exemplo substitui valores na coluna **DaysToManufacture** . A coluna tem um tipo de dados Integer e a expressão inclui conversão de **DaysToManufacture** para o tipo de dados DT_WSTR.  
  
```  
REPLACE((DT_WSTR,8)DaysToManufacture,"6","5")  
```  
  
## <a name="see-also"></a>Consulte também  
 [Subcadeia de caracteres &#40;expressão do SSIS&#41;](substring-ssis-expression.md)   
 [Funções &#40;expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
