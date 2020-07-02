---
title: Função Floor (XQuery) | Microsoft Docs
description: Saiba mais sobre a função XQuery Floor () que retorna o maior número sem nenhuma parte de fração que não seja maior que o valor de seu argumento.
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- floor function [XQuery]
- fn:floor function
ms.assetid: 4ace57dd-b66e-4b60-a2b9-a1b0f1a0831d
author: rothja
ms.author: jroth
ms.openlocfilehash: cf7943cbcef462dbdf73e72357f28e4f4e3eb20d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85724210"
---
# <a name="numeric-values-functions---floor"></a>Funções de Valores Numéricos – floor
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Retorna o maior número sem parte de fração que não seja maior que o valor de seu argumento. Se o argumento for uma sequência vazia, ele retornará a sequência vazia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:floor ($arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Número ao qual a função é aplicada.  
  
## <a name="remarks"></a>Comentários  
 Se o tipo de *$ARG* for um dos três tipos de base numéricos, **xs: float**, **xs: Double**ou **xs: decimal**, o tipo de retorno será o mesmo que o tipo de *$ARG* . Se o tipo de *$ARG* for um tipo derivado de um dos tipos numéricos, o tipo de retorno será o tipo numérico base.  
  
 Se a entrada nas funções fn: Floor, fn: teto ou fn: round for **xdt: untypedAtomic**, dados não tipados, ela será convertida implicitamente em **xs: Double**. Qualquer outro tipo gera um erro estático.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são armazenadas em várias colunas de tipo **XML** no banco de dados de exemplo AdventureWorks.  
  
 Você pode usar o exemplo de trabalho na [função de teto (XQuery)](../xquery/numeric-values-functions-ceiling.md) para a função de base do XQuery **()** . Tudo o que você precisa fazer é substituir a função de **teto ()** na consulta pela função **Floor ()** .  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   A função **Floor ()** mapeia todos os valores inteiros para xs: decimal.  
  
## <a name="see-also"></a>Consulte Também  
 [Função de teto &#40;&#41;XQuery](../xquery/numeric-values-functions-ceiling.md)   
 [Função round &#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)   
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
