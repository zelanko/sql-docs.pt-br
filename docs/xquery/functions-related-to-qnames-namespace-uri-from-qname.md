---
title: namespace-URI-from-QName (XQuery) | Microsoft Docs
description: Saiba como usar a função namespace-URI-from-QName para recuperar o URI de namespace de um QName.
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri-from-QName function
- namespace-uri-from-QName function
ms.assetid: 4ab3f003-2a3b-4268-9e88-b615e35701b2
author: rothja
ms.author: jroth
ms.openlocfilehash: 035b92b719431b5a9b74f951f20d51911a41d59c
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035764"
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>Funções Relacionadas a QNames – namespace-uri-from-QName
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Retorna uma cadeia de caracteres que representa o URI do namespace do QName especificado por *$ARG*. O resultado será a sequência vazia se *$ARG* for a sequência vazia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 É o QName cujo namespace-uri é retornado.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são armazenadas em várias colunas de tipo **XML** no banco de dados AdventureWorks.  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>a. Recuperar o URI do namespace de um QName  
 Para obter um exemplo funcional, consulte [local-name-from-QName &#40;&#41;XQuery ](../xquery/functions-related-to-qnames-local-name-from-qname.md).  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   A função **namespace-URI-from-QName ()** retorna instâncias de xs: String em vez de xs: anyURI.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções relacionadas a QNames &#40;&#41;XQuery ](./functions-related-to-qnames-expanded-qname.md)  
  
