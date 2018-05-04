---
title: namespace-uri-de-QName (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- fn:namespace-uri-from-QName function
- namespace-uri-from-QName function
ms.assetid: 4ab3f003-2a3b-4268-9e88-b615e35701b2
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f18e99e48ec910c4625a34456aebcc4ab18c8b99
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>Funções relacionadas a QNames - namespace uri do QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna uma cadeia de caracteres que representa o uri de namespace do QName especificado por *$arg*. O resultado será a sequência vazia se *$arg* é a sequência vazia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 É o QName cujo namespace-uri é retornado.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em instâncias XML que são armazenados em várias **xml** colunas de tipo de banco de dados AdventureWorks.  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>A. Recuperar o URI do namespace de um QName  
 Para obter um exemplo de funcionamento, consulte [nome local do QName &#40;XQuery&#41;](../xquery/functions-related-to-qnames-local-name-from-qname.md).  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   O **namespace-uri-from-QName()** função retorna instâncias de xs: String em vez de xs: anyURI.  
  
## <a name="see-also"></a>Consulte também  
 [Funções relacionadas a QNames &#40;XQuery&#41;](http://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
