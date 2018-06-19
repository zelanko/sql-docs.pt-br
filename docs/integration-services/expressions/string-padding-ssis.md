---
title: Preenchimento de cadeia (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- padding strings [Integration Services]
- expressions [Integration Services], string padding
- string padding
ms.assetid: d3fed73d-e0d4-4c67-9355-fb7083a72dd6
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 42475dee286509ef292a5567226bb152af42762e
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35400378"
---
# <a name="string-padding-ssis"></a>Preenchimento de cadeia (SSIS)
  O avaliador de expressão não verifica se uma cadeia de caracteres contém espaços à esquerda e à direita, e não preenche as cadeias de caracteres para que fiquem com o mesmo comprimento antes de compará-las. Se as expressões exigirem preenchimento de cadeia de caracteres, você poderá usar o operador + para concatenar valores de coluna e cadeias de caracteres vazias. Para obter mais informações, consulte [+ &#40;Concatenar&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/concatenate-ssis-expression.md).  
  
 Por ouro lado, se você quiser remover espaços, o avaliador de expressão fornece as funções LTRIM, RTRIM e TRIM, que removem os espaços à esquerda e/ou à direita. Para obter mais informações, consulte [LTRIM &#40;Expressão SSIS&#41;](../../integration-services/expressions/ltrim-ssis-expression.md), [RTRIM &#40;Expressão SSIS&#41;](../../integration-services/expressions/rtrim-ssis-expression.md) e [TRIM &#40;Expressão SSIS&#41;](../../integration-services/expressions/trim-ssis-expression.md).  
  
> [!NOTE]  
>  A função LEN inclui espaços em branco à esquerda e à direita em sua conta.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Artigo técnico, [SSIS Expression Cheat Sheet](http://go.microsoft.com/fwlink/?LinkId=746575), em pragmaticworks.com  
  
  
