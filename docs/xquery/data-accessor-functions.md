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
ms.workload: Inactive
ms.openlocfilehash: f70f14b553182c4f52d9c27ec0972fd3d5978026
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
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
  
  
