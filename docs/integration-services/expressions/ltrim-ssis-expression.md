---
title: "LTRIM (Express&#227;o SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "espaços em branco à esquerda"
  - "função LTRIM"
ms.assetid: d082f42a-d7e7-49f5-a503-ac44ba630832
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# LTRIM (Express&#227;o SSIS)
  Retorna uma expressão de caractere depois de remover espaços em branco à esquerda.  
  
> [!NOTE]  
>  LTRIM não remove caracteres do espaço em branco como os caracteres de guia ou de alimentação de linha. Unicode fornece pontos de código para muitos tipos diferentes de espaços, mas essa função reconhece somente o ponto de código Unicode 0x0020. Quando as cadeias de caracteres de DBCS (Conjunto de caracteres de byte duplo) são convertidas para Unicode, elas podem incluir caracteres de espaço diferentes de 0x0020, e a função não pode remover esses espaços. Para remover todos os tipos de espaços, você poderá usar o método LTrim do Microsoft Visual Basic .NET em uma execução de script a partir do componente Script.  
  
## Sintaxe  
  
```  
  
LTRIM(character expression)  
```  
  
## Argumentos  
 *character_expression*  
 É uma expressão de caractere da qual remover espaços.  
  
## Tipos de resultado  
 DT_WSTR  
  
## Comentários  
 LTRIM só funciona com o tipo de dados DT_WSTR. Um argumento *character_expression* que é um literal de cadeia de caracteres ou uma coluna de dados com o tipo de dados DT_STR é implicitamente convertido para o tipo de dados DT_WSTR antes de LTRIM executar sua operação. Outros tipos de dados devem ser explicitamente convertidos para o tipo de dados DT_WSTR. Para obter mais informações, consulte [Tipos de dados do Integration Services](../../integration-services/data-flow/integration-services-data-types.md) e [Cast &#40;Expressão SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 LTRIM retornará um resultado nulo se o argumento for nulo.  
  
## Exemplos de expressões  
 Este exemplo remove espaços à esquerda de um literal de cadeia de caracteres. O resultado de retorno é "Hello".  
  
```  
LTRIM("    Hello")  
```  
  
 Este exemplo remove espaços à esquerda da coluna **FirstName** .  
  
```  
LTRIM(FirstName)  
```  
  
 Este exemplo remove os espaços à esquerda da variável **FirstName** .  
  
```  
LTRIM(@FirstName)  
```  
  
## Consulte também  
 [RTRIM &#40;Expressão SSIS&#41;](../../integration-services/expressions/rtrim-ssis-expression.md)   
 [TRIM &#40;Expressão SSIS&#41;](../../integration-services/expressions/trim-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  