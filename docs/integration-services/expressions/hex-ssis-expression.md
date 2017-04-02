---
title: "HEX (Express&#227;o SSIS) | Microsoft Docs"
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
  - "dados hexadecimais"
  - "função HEX"
ms.assetid: f5d471ee-aeef-421c-b6e1-55b9676c3842
caps.latest.revision: 36
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 36
---
# HEX (Express&#227;o SSIS)
  Retorna uma cadeia de caracteres que representa o valor hexadecimal de um inteiro.  
  
## Sintaxe  
  
```  
  
HEX(integer_expression)  
```  
  
## Argumentos  
 *integer_expression*  
 É um inteiro assinado ou não assinado.  
  
## Tipos de resultado  
 DT_WSTR  
  
## Comentários  
 HEX retornará nulo se *integer_expression* for nulo.  
  
 O argumento *integer_expression* deve ser avaliado como um inteiro. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 O resultado de retorno não inclui qualificadores como o prefixo 0x. Para incluir um prefixo, use o operador + (Concatenar). Para obter mais informações, consulte [+ &#40;Concatenar&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/concatenate-ssis-expression.md).  
  
 As letras A – F, usadas em notações HEX, são exibidas em letras maiúsculas.  
  
 O tamanho da cadeia de caracteres resultante para tipos de dados inteiro é:  
  
-   DT_I1 e DT_UI1 retornam uma cadeia de caracteres com um comprimento máximo de 2.  
  
-   DT_I2 e DT_UI2 retornam uma cadeia de caracteres com um comprimento máximo de 4.  
  
-   DT_I4 e DT_UI4 retornam uma cadeia de caracteres com um comprimento máximo de 8.  
  
-   DT_I8 e DT_UI8 retornam uma cadeia de caracteres com um comprimento máximo de 16.  
  
## Exemplos de expressões  
 Esse exemplo usa um literal numérico. A função retorna o valor 190.  
  
```  
HEX(400)   
```  
  
 Esse exemplo usa a coluna **ReorderPoint**. O tipo de dados da coluna é **smallint**. Se **ReorderPoint** for 750, a função retornará 2EE.  
  
```  
HEX(ReorderPoint)   
```  
  
 Esse exemplo usa **LocaleID**, uma variável de sistema. Se **LocaleID** for 1033, a função retornará 409.  
  
```  
HEX(@LocaleID)  
```  
  
## Consulte também  
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  