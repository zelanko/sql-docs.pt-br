---
title: "Expressões aritméticas (XQuery) | Microsoft Docs"
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
- expressions [XQuery], arithmetic
- arithmetic expressions
ms.assetid: 90d675bf-56da-459a-9771-8cd13920a9fc
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6ba5c642195f1049f7df59a0fa14ef666eec4bfe
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="arithmetic-expressions-xquery"></a>Expressões aritméticas (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Há suporte para todos os operadores aritméticos, exceto para **idiv**. Os exemplos a seguir ilustram o uso básico dos operadores aritméticos:  
  
```  
DECLARE @x xml  
SET @x=''  
SELECT @x.query('2 div 2')  
SELECT @x.query('2 * 2')  
```  
  
 Porque **idiv** não é tem suporte, uma solução é usar o **xs:integer()** construtor:  
  
```  
DECLARE @x xml  
SET @x=''  
-- Following will not work  
-- SELECT @x.query('2 idiv 2')  
-- Workaround   
SELECT @x.query('xs:integer(2 div 3)')  
```  
  
 O tipo resultante de um operador aritmético é baseado nos tipos dos valores de entrada. Se os operandos forem de tipos diferentes, qualquer um dos dois, ou ambos, quando necessário serão convertidos em um tipo de base primitivo comum, de acordo com a hierarquia do tipo. Para obter informações sobre hierarquia de tipo, consulte [regras de conversão de tipo em XQuery](../xquery/type-casting-rules-in-xquery.md).  
  
 Promoção de tipo numérico ocorre se as duas operações forem de tipos de base numéricos diferentes. Por exemplo, adicionando um **xs: decimal** para um **xs: Double** alteraria primeiro o valor decimal para um duplo. Em seguida, a adição seria executada de forma a resultar em um valor duplo.  
  
 Valores atômicos não digitados são convertidos para o tipo de base numérica do outro operando, ou para **xs: Double** se o outro operando também não for digitado.  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   Argumentos para os operadores aritméticos devem ser do tipo numérico ou **untypedAtomic**.  
  
-   Operações em **xs: Integer** valores resultam em um valor do tipo **xs: decimal** em vez de **xs: Integer**.  
  
  
