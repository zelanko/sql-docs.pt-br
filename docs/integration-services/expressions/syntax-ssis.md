---
title: "Sintaxe (SSIS) | Microsoft Docs"
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
  - "expressões [Integration Services], sintaxe"
  - "sintaxe [Integration Services]"
ms.assetid: 61c053c5-1182-4ad0-b804-51cbd19aa0ba
caps.latest.revision: 48
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 48
---
# Sintaxe (SSIS)
  A sintaxe de expressão [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é semelhante à sintaxe que as linguagens C e C# usam. Expressões incluem elementos como identificadores (colunas e variáveis), literais, operadores e funções. Este tópico resume os requisitos exclusivos da sintaxe do avaliador de expressão como eles se aplicam a diferentes elementos de expressão.  
  
> [!NOTE]  
>  Em versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], havia um limite de 4000 caracteres no resultado da avaliação de uma expressão quando o resultado incluía o tipo de dados DT_WSTR ou DT_STR do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Esse limite foi removido.  
  
 Para obter expressões de amostra que utilizam operadores e funções específicos, consulte o tópico sobre cada operador e função: [Operadores &#40;Expressão SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md) e [Funções &#40;Expressão SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md).  
  
 Para obter expressões de amostra que usam os vários operadores e funções como também identificadores e literais, consulte [Exemplos de expressões avançadas do Integration Services](../../integration-services/expressions/examples-of-advanced-integration-services-expressions.md).  
  
 Para ver exemplos de expressões para usar em expressões de propriedade, consulte [Usar expressões de propriedade em pacotes](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
## Identificadores  
 Expressões podem incluir identificadores de coluna e variável. As colunas podem ter origem na fonte de dados ou podem ser criadas através de transformações no fluxo de dados. Expressões podem usar identificadores de linhagem para fazer referência a colunas. Identificadores de linhagem são números que identifique exclusivamente elementos de pacote. Identificadores de linhagem, referenciados em uma expressão, devem incluir um prefixo de libra (#). Por exemplo, o identificador de linhagem 138 é referenciado utilizando #138.  
  
 Expressões podem incluir as variáveis de sistema que o [!INCLUDE[ssIS](../../includes/ssis-md.md)] fornece e variáveis personalizadas. Variáveis, quando referenciadas em uma expressão, devem incluir o prefixo @. Por exemplo, a variável `Counter` é referenciada utilizando @ Counter. O caractere @ não faz parte do nome de variável; só indica para o avaliador de expressão que o identificador é uma variável. Para obter mais informações, consulte [Identificadores &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md).  
  
## Literais  
 Expressões podem incluir literais numérico, de cadeia de caracteres e boolianos. Literais de cadeia de caracteres utilizados em expressões devem ser colocados entre aspas. Literais numéricos e boolianos não têm aspa. A linguagem de expressão inclui sequências de escape para caracteres que frequentemente escapam. Para obter mais informações, consulte [Literais &#40;SSIS&#41;](../../integration-services/expressions/literals-ssis.md).  
  
## Operadores  
 O avaliador de expressão fornece um conjunto de operadores que fornece funcionalidade semelhante ao conjunto de operadores em linguagens como Transact-SQL, C++ e C#. Porém, a linguagem de expressão inclui os operadores adicionais e usa símbolos diferentes daqueles com os quais pode estar familiarizado. Para obter mais informações, consulte [Operadores &#40;Expressão SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md).  
  
### Operador de resolução de namespace  
 Expressões usam o operador de resolução de namespace (::) para resolver a ambiguidade de variáveis que têm o mesmo nome. Utilizando o operador de resolução de namespace, você pode qualificar a variável com seu namespace, que o possibilita utilizar diversas variáveis com o mesmo nome em um pacote.  
  
#### Operador cast  
 O operador cast converte os resultados da expressão, os valores de coluna e de variáveis e as constantes de um tipo de dados para outro. O operador cast fornecido pela linguagem da expressão é semelhante àquela fornecida pelas linguagens C e C#. Em Transact-SQL, as funções CAST e CONVERT fornecem essa funcionalidade. A sintaxe do operador cast é diferente daquelas usadas por CAST e CONVERT dos modos seguintes:  
  
-   Ele pode usar uma expressão como um argumento.  
  
-   Sua sintaxe não inclui a palavra-chave CAST.  
  
-   Sua sintaxe não inclui a palavra-chave AS.  
  
##### Operador condicional  
 O operador condicional retorna uma de duas expressões, com base na avaliação de uma expressão booliana. O operador condicional fornecido pela linguagem da expressão é semelhante àquele fornecida pelas linguagens C e C#. Em expressões multidimensionais (MDX), a função IIF fornece funcionalidade semelhante.  
  
###### Operadores lógicos  
 A linguagem de expressão dá suporte ao caractere ! para o operador lógico NOT. No Transact-SQL, o operador ! é criado no conjunto de operadores relacionais. Por exemplo, Transact-SQL fornece os operadores > e !>. A linguagem de expressão [!INCLUDE[ssIS](../../includes/ssis-md.md)] não aceita a combinação do operador ! e outros operadores. Por exemplo, não é válido a associação de ! e > em !>. Entretanto, a linguagem de expressão oferece suporte a uma combinação interna de caracteres != para a comparação "é diferente de".  
  
###### Operadores de igualdade  
 A gramática do avaliador de expressão fornece o operador de igualdade == . Este operador é o equivalente ao operador = em Transact-SQL e ao operador == em C#.  
  
## Funções  
 A linguagem de expressão inclui funções de data e hora, funções matemáticas e de cadeia de caracteres que são semelhantes às funções Transact-SQL e aos métodos C#.  
  
 Algumas funções têm os mesmos nomes que as funções do Transact-SQL, mas têm funcionalidade um pouco diferente no avaliador de expressão.  
  
-   Em Transact-SQL, a função ISNULL substitui os valores nulo pelo um valor especificado, embora a função ISNULL do avaliador de expressão retorne um booliano com base em uma expressão nula ou não.  
  
-   Em Transact-SQL, a função ROUND inclui uma opção para truncar o conjunto de resultados, embora a função ROUND do avaliador de expressão não inclua.  
  
 Para obter mais informações, consulte [Funções &#40;Expressão SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md).  
  
## Tarefas relacionadas  
 [Usar uma expressão em um componente de fluxo de dados](../Topic/Use%20an%20Expression%20in%20a%20Data%20Flow%20Component.md)  
  
## Conteúdo relacionado  
  
-   Artigo técnico, [SSIS Expression Cheat Sheet](http://go.microsoft.com/fwlink/?LinkId=746575), em pragmaticworks.com  
  
-   Artigo técnico, [Exemplos de expressões SSIS](http://go.microsoft.com/fwlink/?LinkId=220761), em social.technet.microsoft.com  
  
  