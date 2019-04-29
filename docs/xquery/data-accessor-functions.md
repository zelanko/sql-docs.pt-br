---
title: Funções do acessador de dados | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 1c28f61a39e45ea101f2e999d5787dfa23cb29c2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935311"
---
# <a name="data-accessor-functions"></a>Funções do acessador de dados
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Os tópicos nesta seção abordam e proveem código de exemplo para as funções do acessador de dados.  
  
## <a name="understanding-fndata-fnstring-and-text"></a>Compreendendo fn:data (), fn:string () e text()  
 XQuery tem uma função **fn** para extrair valores digitados escalares de nós, um teste de nó **Text ()** para retornar os nós de texto e a função **fn:string()** que retorna o valor de cadeia de caracteres de um nó. Sua utilização pode ser confusa. A seguir são apresentadas diretrizes para usá-las corretamente em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A instância XML \<idade > 12 \< /idade > é usado para fins de ilustração.  
  
-   XML não digitado: A expressão de caminho /age/Text () retorna o nó de texto "12". A função fn:data(/age) retorna o valor "12" da cadeia de caracteres e assim também o faz fn:string (/age).  
  
-   XML digitado: A expressão /age/Text () retorna um erro estático para qualquer tipada simples \<idade > elemento. Por outro lado, fn:data(/age) retorna o número inteiro 12. A fn:string(/age) resulta na cadeia de caracteres "12".  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Função de cadeia de caracteres &#40;XQuery&#41;](../xquery/data-accessor-functions-string-xquery.md)  
  
-   [Função de dados &#40;XQuery&#41;](../xquery/data-accessor-functions-data-xquery.md)  
  
## <a name="see-also"></a>Consulte também  
 [Expressões de caminho &#40;XQuery&#41;](../xquery/path-expressions-xquery.md)  
  
  
