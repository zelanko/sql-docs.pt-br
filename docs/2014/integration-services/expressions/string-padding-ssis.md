---
title: Preenchimento de cadeia (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- padding strings [Integration Services]
- expressions [Integration Services], string padding
- string padding
ms.assetid: d3fed73d-e0d4-4c67-9355-fb7083a72dd6
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b95eed3c086b0d9e07feb11c353e90cece56a18e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37152877"
---
# <a name="string-padding-ssis"></a>Preenchimento de cadeia (SSIS)
  O avaliador de expressão não verifica se uma cadeia de caracteres contém espaços à esquerda e à direita, e não preenche as cadeias de caracteres para que fiquem com o mesmo comprimento antes de compará-las. Se as expressões exigirem preenchimento de cadeia de caracteres, você poderá usar o operador + para concatenar valores de coluna e cadeias de caracteres vazias. Para obter mais informações, consulte [+ &#40;Concatenar&#41; &#40;Expressão SSIS&#41;](concatenate-ssis-expression.md).  
  
 Por ouro lado, se você quiser remover espaços, o avaliador de expressão fornece as funções LTRIM, RTRIM e TRIM, que removem os espaços à esquerda e/ou à direita. Para obter mais informações, consulte [LTRIM &#40;Expressão SSIS&#41;](trim-ssis-expression.md), [RTRIM &#40;Expressão SSIS&#41;](rtrim-ssis-expression.md) e [TRIM &#40;Expressão SSIS&#41;](trim-ssis-expression.md).  
  
> [!NOTE]  
>  A função LEN inclui espaços em branco à esquerda e à direita em sua conta.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Artigo técnico, [SSIS Expression Cheat Sheet](http://go.microsoft.com/fwlink/?LinkId=217683), em pragmaticworks.com  
  
  
