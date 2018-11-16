---
title: Expressões de caminho (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- path expressions [XQuery]
- expressions [XQuery], path
ms.assetid: b93fa36c-bf69-46b9-b137-f597d66fd0c0
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: fdc9279d821402e0011b10ef4c1843a721178a9f
ms.sourcegitcommit: 0f7cf9b7ab23df15624d27c129ab3a539e8b6457
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51291422"
---
# <a name="path-expressions-xquery"></a>Expressões de caminho (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  As expressões de caminho XQuery localizam nós, como elemento, atributo e nós de texto, em um documento. O resultado de uma expressão de caminho sempre ocorre na ordem do documento sem duplicar nós na sequência de resultado. Ao especificar um caminho, você pode usar uma sintaxe abreviada ou não. As informações a seguir têm o foco na sintaxe não abreviada. A sintaxe abreviada é descrita posteriormente neste tópico.  
  
> [!NOTE]  
>  Porque as consultas de exemplo neste tópico são especificadas em relação a **xml** colunas de tipo **CatalogDescription** e **instruções**, no  **ProductModel** tabela, você deve se familiarizar com o conteúdo e a estrutura dos documentos XML armazenados nessas colunas.  
  
 Uma expressão de caminho pode ser relativa ou absoluta. É apresentada a seguir uma descrição de ambas:  
  
-   Uma expressão de caminho relativa é composta por uma ou mais etapas separadas por uma ou duas barras (/ ou / /). Por exemplo, `child::Features` é uma expressão de caminho relativa, onde `Child` refere-se somente a nós filho do nó de contexto. Esse é o nó que está sendo processado atualmente. A expressão recupera o \<recursos > filhos do nó do elemento do nó de contexto.  
  
-   Uma expressão de caminho absoluta inicia com uma ou duas barras (/ ou / /), seguidas por um caminho relativo opcional. Por exemplo, a barra inicial na expressão, `/child::ProductDescription`, indica que é uma expressão de caminho absoluta. Como uma marca de barra "/" no início de uma expressão retorna o nó de raiz do documento do nó de contexto, a expressão retorna todos os \<ProductDescription > elementos filho do nó da raiz do documento.  
  
     Se um caminho absoluto iniciar com uma única barra, ele poderá ou não ser seguido por um caminho relativo. Se você especificar só uma barra, a expressão retornará o nó raiz do nó de contexto. Para um tipo de dados XML, esse é seu nó do documento.  
  
 Uma expressão de caminho característica é composta por etapas. Por exemplo, a expressão de caminho absoluto, `/child::ProductDescription/child::Summary`, contém duas etapas separadas por uma barra.  
  
-   A primeira etapa recupera os \<ProductDescription > elementos filho do nó da raiz do documento.  
  
-   A segunda etapa recupera os \<Summary > filhos do nó do elemento para cada recuperados \<ProductDescription > nó de elemento, que por sua vez se torna o nó de contexto.  
  
 Uma etapa em uma expressão de caminho pode ser uma etapa de eixo ou uma etapa geral.  
  
## <a name="axis-step"></a>Etapa de eixo  
 Uma etapa de eixo em uma expressão de caminho tem as seguintes partes.  
  
 [axis](../xquery/path-expressions-specifying-axis.md)  
 Define a direção de movimento. Uma etapa de eixo em uma expressão de caminho que inicia no nó de contexto e navega para esses nós que são atingíveis na direção especificada pelo eixo.  
  
 [teste de nó](../xquery/path-expressions-specifying-node-test.md)  
 Especifica o tipo de nó ou nomes de nó a serem selecionados.  
  
 Zero ou mais predicados opcionais  
 Filtra os nós selecionando alguns e descartando outros.  
  
 Os exemplos seguintes usam um **axisstep** nas expressões de caminho:  
  
-   A expressão de caminho absoluta, `/child::ProductDescription`, contém só uma etapa. Especifica um eixo (`child`) e um teste de nó (`ProductDescription`).  
  
-   A expressão de caminho relativa, `child::ProductDescription/child::Features`, contém duas etapas separadas por uma barra. Ambas as etapas especificam um eixo filho. ProductDescription e Features são testes de nó.  
  
-   A expressão de caminho relativo, `child::root/child::Location[attribute::LocationID=10]`, contém duas etapas separadas por uma barra. A primeira etapa especifica um eixo (`child`) e um teste de nó (`root`). A segunda etapa especifica todos os três componentes de uma etapa de eixo: um eixo (filho), um teste de nó (`Location`) e um predicado (`[attribute::LocationID=10]`).  
  
 Para obter mais informações sobre os componentes de uma etapa de eixo, consulte [especificando eixo em uma etapa de expressão de caminho](../xquery/path-expressions-specifying-axis.md), [especificando Node Test em uma etapa de expressão de caminho](../xquery/path-expressions-specifying-node-test.md), e [especificando predicados em uma Etapa de expressão de caminho](../xquery/path-expressions-specifying-predicates.md).  
  
## <a name="general-step"></a>Etapa geral  
 Uma etapa geral é apenas uma expressão que deve ser avaliada em uma sequência de nós.  
  
 A implementação XQuery no SQL Server oferece suporte a uma etapa geral, como a primeira etapa em uma expressão de caminho. São apresentados a seguir exemplos de expressões de caminho que usam etapas gerais.  
  
```  
(/a, /b)/c  
id(/a/b)  
```  
  
 Para obter mais informações sobre a função id, consulte [id da função &#40;XQuery&#41;](../xquery/functions-on-sequences-id.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Especificação de eixo em uma etapa de expressão de caminho](../xquery/path-expressions-specifying-axis.md)  
 Descreve o funcionamento com a etapa de eixo em uma expressão de caminho.  
  
 [Especificando Node Test em uma etapa de expressão de caminho](../xquery/path-expressions-specifying-node-test.md)  
 Descreve o funcionamento com testes de nó em uma expressão de caminho.  
  
 [Especificando predicados em uma etapa de expressão de caminho](../xquery/path-expressions-specifying-predicates.md)  
 Descreve o funcionamento com predicados em uma expressão de caminho.  
  
 [Usando sintaxe abreviada em uma expressão de caminho](../xquery/path-expressions-using-abbreviated-syntax.md)  
 Descreve o funcionamento com sintaxe abreviada em uma expressão de caminho.  
  
  
