---
title: "RTRIM (Express&#227;o SSIS) | Microsoft Docs"
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
  - "função RTRIM"
  - "espaços em branco à direita"
ms.assetid: 529bd43e-3f8a-4682-a33e-569176aa7fc4
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# RTRIM (Express&#227;o SSIS)
  Retorna uma expressão character depois de remover espaços em branco à direita.  
  
> [!NOTE]  
>  RTRIM não remove caracteres do espaço em branco como os caracteres de guia ou de alimentação de linha. Unicode fornece pontos de código para muitos tipos diferentes de espaços, mas essa função reconhece somente o ponto de código Unicode 0x0020. Quando as cadeias de caracteres de DBCS (Conjunto de caracteres de byte duplo) são convertidas para Unicode, elas podem incluir caracteres de espaço diferentes de 0x0020, e a função não pode remover esses espaços. Para remover todos os tipos de espaços, você poderá usar o método RTrim do Microsoft Visual Basic .NET em uma execução de script a partir do componente Script.  
  
## Sintaxe  
  
```  
  
RTRIM(character expression)  
```  
  
## Argumentos  
 *character_expression*  
 É uma expressão de caractere da qual remover espaços.  
  
## Tipos de resultado  
 DT_WSTR  
  
## Comentários  
 RTRIM só funciona com o tipo de dados DT_WSTR. Um argumento *character_expression* que é um literal de cadeia de caracteres ou uma coluna de dados com o tipo de dados DT_STR é implicitamente convertido para o tipo de dados DT_WSTR antes de RTRIM executar sua operação. Outros tipos de dados devem ser explicitamente convertidos para o tipo de dados DT_WSTR. Para obter mais informações, consulte [Tipos de dados do Integration Services](../../integration-services/data-flow/integration-services-data-types.md) e [Cast &#40;Expressão SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 RTRIM retornará um resultado nulo se o argumento for nulo.  
  
## Exemplos de expressões  
 Este exemplo remove espaços à direita de um literal de cadeia de caracteres. O resultado de retorno é "Hello".  
  
```  
RTRIM("Hello   ")  
```  
  
 Este exemplo remove espaços à direita de uma concatenação das colunas **FirstName** e **LastName** .  
  
```  
RTRIM(FirstName + " " + LastName)  
```  
  
 Este exemplo remove os espaços à direita da variável **FirstName** .  
  
```  
RTRIM(@FirstName)  
```  
  
## Consulte também  
 [LTRIM &#40;Expressão SSIS&#41;](../../integration-services/expressions/ltrim-ssis-expression.md)   
 [TRIM &#40;Expressão SSIS&#41;](../../integration-services/expressions/trim-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  