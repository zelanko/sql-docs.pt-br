---
title: TRIM (expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- leading blanks
- TRIM function
- trailing blanks
ms.assetid: 7dd9081d-a3d4-483a-bf7e-bf2bd7692d39
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 63154693a20922201e7138d8e03a0609fe04b4df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967669"
---
# <a name="trim-ssis-expression"></a>TRIM (Expressão SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Retorna uma expressão de caractere depois de remover espaços em branco à esquerda e direita.  
  
> [!NOTE]  
>  TRIM não remove caracteres do espaço em branco como os caracteres de guia ou de alimentação de linha. Unicode fornece pontos de código para muitos tipos diferentes de espaços, mas essa função reconhece somente o ponto de código Unicode 0x0020. Quando as cadeias de caracteres de DBCS (Conjunto de caracteres de byte duplo) são convertidas para Unicode, elas podem incluir caracteres de espaço diferentes de 0x0020, e a função não pode remover esses espaços. Para remover todos os tipos de espaços, você poderá usar o método Trim do Microsoft Visual Basic .NET em uma execução de script a partir do componente Script.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TRIM(character_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É uma expressão de caractere da qual remover espaços.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 TRIM retornará um resultado nulo se o argumento for nulo.  
  
 TRIM só funciona com o tipo de dados DT_WSTR. Um argumento *character_expression* que é um literal de cadeia de caracteres ou uma coluna de dados com o tipo de dados DT_STR é implicitamente convertido para o tipo de dados DT_WSTR antes de TRIM executar sua operação. Outros tipos de dados devem ser explicitamente convertidos para o tipo de dados DT_WSTR. Para obter mais informações, consulte [Tipos de dados do Integration Services](../../integration-services/data-flow/integration-services-data-types.md) e [Cast &#40;Expressão SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo remove espaços à direita e à esquerda de um literal de cadeia de caracteres. O resultado de retorno é "Nova Iorque".  
  
```  
TRIM("   New York   ")  
```  
  
 Este exemplo remove espaços à direita e à esquerda do resultado da concatenação das colunas **FirstName** e **LastName** . A cadeia de caracteres vazia entre **FirstName** e **LastName** não é removida.  
  
```  
TRIM(FirstName + " "+ LastName)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [LTRIM &#40;Expressão SSIS&#41;](../../integration-services/expressions/ltrim-ssis-expression.md)   
 [RTRIM &#40;Expressão SSIS&#41;](../../integration-services/expressions/rtrim-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
