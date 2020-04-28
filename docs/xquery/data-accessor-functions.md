---
title: Funções de acessador de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- data-accessor functions [XQuery]
ms.assetid: 31bad04f-7c74-4773-9f83-612704fdd21c
author: rothja
ms.author: jroth
ms.openlocfilehash: b3726686a2c0e5229a0fccf4d9f51c0e1404f1a3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68038955"
---
# <a name="data-accessor-functions"></a>Funções do acessador de dados
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Os tópicos nesta seção abordam e proveem código de exemplo para as funções do acessador de dados.  
  
## <a name="understanding-fndata-fnstring-and-text"></a>Compreendendo fn:data (), fn:string () e text()  
 O XQuery tem uma função **fn: data ()** para extrair valores digitados, com tipos de nós, um texto de teste de nó **()** para retornar nós de texto e a função **fn: String ()** que retorna o valor da cadeia de caracteres de um nó. Sua utilização pode ser confusa. A seguir são apresentadas diretrizes para usá-las corretamente em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A idade da \<instância XML>\<12/age> é usada para fins de ilustração.  
  
-   XML não digitado: a expressão de caminho /age/text() retorna o nó de texto "12". A função fn:data(/age) retorna o valor "12" da cadeia de caracteres e assim também o faz fn:string (/age).  
  
-   XML tipado: a expressão/age/text () retorna um erro estático para qualquer elemento \<de> age de tipo simples. Por outro lado, fn:data(/age) retorna o número inteiro 12. A fn:string(/age) resulta na cadeia de caracteres "12".  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Função de cadeia de caracteres &#40;XQuery&#41;](../xquery/data-accessor-functions-string-xquery.md)  
  
-   [Função de dados &#40;&#41;XQuery](../xquery/data-accessor-functions-data-xquery.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões de caminho &#40;&#41;XQuery](../xquery/path-expressions-xquery.md)  
  
  
