---
title: Funções do acessador de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- data-accessor functions [XQuery]
ms.assetid: 31bad04f-7c74-4773-9f83-612704fdd21c
caps.latest.revision: 30
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a18880a2419467bdd7abe8ab8830af81faae69f6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="data-accessor-functions"></a>Funções do acessador de dados
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Os tópicos nesta seção abordam e proveem código de exemplo para as funções do acessador de dados.  
  
## <a name="understanding-fndata-fnstring-and-text"></a>Compreendendo fn:data (), fn:string () e text()  
 XQuery tem uma função **fn** para extrair valores digitados escalares de nós, um teste de nó **Text ()** para retornar nós de texto e a função **fn:string()** que retorna o valor de cadeia de caracteres de um nó. Sua utilização pode ser confusa. A seguir são apresentadas diretrizes para usá-las corretamente em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A instância XML \<age > 12 \< /age > é usado para fins de ilustração.  
  
-   XML não digitado: a expressão de caminho /age/text() retorna o nó de texto "12". A função fn:data(/age) retorna o valor "12" da cadeia de caracteres e assim também o faz fn:string (/age).  
  
-   XML digitado: A expressão /age/Text () retorna um erro estático para qualquer tipado simples \<idade > elemento. Por outro lado, fn:data(/age) retorna o número inteiro 12. A fn:string(/age) resulta na cadeia de caracteres "12".  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Função String &#40;XQuery&#41;](../xquery/data-accessor-functions-string-xquery.md)  
  
-   [Função data &#40;XQuery&#41;](../xquery/data-accessor-functions-data-xquery.md)  
  
## <a name="see-also"></a>Consulte também  
 [Expressões de caminho &#40;XQuery&#41;](../xquery/path-expressions-xquery.md)  
  
  
