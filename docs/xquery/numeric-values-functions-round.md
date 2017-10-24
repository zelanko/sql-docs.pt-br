---
title: "Função Round (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- fn:round function
- round function [XQuery]
ms.assetid: 320b572f-bd5b-4055-95a6-dec5718c0041
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 84815a954021f755173fefd60ef174e7a0acdcf1
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="numeric-values-functions---round"></a>Funções de valores numéricas - arredondar
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna o número que não tem uma parte fracionária mais próxima do argumento. Se houver mais de um número semelhante a esse, o que for mais próximo ao infinito positivo será retornado. Por exemplo:  
  
 Se o argumento for 2.5, **Round ()** retorna 3.  
  
 Se o argumento for 2.4999, **Round ()** retorna 2.  
  
 Se o argumento for -2.5, **Round ()** retorna -2.  
  
 Se o argumento for uma sequência vazia, **Round ()** retornará a sequência vazia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:round ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Número ao qual a função é aplicada.  
  
## <a name="remarks"></a>Comentários  
 Se o tipo de *$arg* é um de três tipos base numéricos, **xs: float**, **xs: Double**, ou **xs: decimal**, o tipo de retorno é igual a *$arg* tipo. Se o tipo de *$arg* é um tipo que é derivado de um dos tipos numéricos, o tipo de retorno é o tipo numérico básico.  
  
 Se a entrada para o **fn: Floor**, **fn: Ceiling**, ou **fn: round** funções é **XDT: untypedatomic**, dados não digitados, ela será convertida implicitamente para **xs: Double**.  
  
 Qualquer outro tipo gera um erro estático.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em instâncias XML armazenadas em várias **xml** colunas de tipo de banco de dados AdventureWorks.  
  
 Você pode usar o exemplo de funcionamento do [função ceiling (XQuery)](../xquery/numeric-values-functions-ceiling.md) para o **Round ()** função XQuery. Tudo o que você precisa fazer é substituir a **Ceiling** função na consulta com o **Round ()** função.  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   O **Round ()** função mapeia os valores inteiros para xs: decimal.  
  
-   O **Round ()** função dos valores xs: Double e xs: float entre - 0.5 E0 e - 0e0 são mapeadas para 0e0 em vez de - 0e0.  
  
## <a name="see-also"></a>Consulte também  
 [Floor função &#40; XQuery &#41;](../xquery/numeric-values-functions-floor.md)   
 [limite de função &#40; XQuery &#41;](../xquery/numeric-values-functions-ceiling.md)  
  
  

