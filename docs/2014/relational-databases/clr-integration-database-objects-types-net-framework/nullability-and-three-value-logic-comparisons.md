---
title: Comparações de lógica de três valores e nulidade | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- precision [CLR integration]
- overflow detections [CLR integration]
- null values [CLR integration]
- three-value logic comparisons [CLR integration]
- data types [CLR integration]
- SqlBoolean data type
ms.assetid: 13da4c7f-1010-4b2d-a63c-c69b6bfd96f1
caps.latest.revision: 39
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 07a0076cadc805b3534d778070b7b61b28e1bf3d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117912"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Comparações de lógica de três valores e nulidade
  Se estiver familiarizado com os tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você achará a semântica e a precisão semelhantes no `System.Data.SqlTypes` namespace de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. No entanto, há algumas diferenças, e este tópico aborda a mais importante delas.  
  
## <a name="null-values"></a>Valores NULL  
 A principal diferença entre os tipos de dados CLR (Common Language Runtime) nativos e os tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é que os primeiros não permitem valores NULL, ao passo que os últimos fornecem uma semântica NULL completa.  
  
 As comparações são afetadas por valores NULL. Durante a comparação entre dois valores x e y, caso x ou y seja NULL, algumas comparações lógicas são avaliadas como UNKNOWN, e não como true ou false.  
  
## <a name="sqlboolean-data-type"></a>Tipo de dados SqlBoolean  
 O namespace `System.Data.SqlTypes` introduz um tipo `SqlBoolean` para representar essa lógica de 3 valores. Comparações entre qualquer `SqlTypes` retornam um tipo de valor `SqlBoolean`. O valor UNKNOWN é representado pelo valor nulo do tipo `SqlBoolean`. São fornecidas as propriedades `IsTrue`, `IsFalse`e `IsNull` para verificar o valor de um tipo `SqlBoolean`.  
  
## <a name="operations-functions-and-null-values"></a>Operações, funções e valores NULL  
 Todos os operadores aritméticos (+, -, \*, /, %), operadores bit a bit (~, &, e |), e a maioria das funções retornam NULL se qualquer um dos operandos ou argumentos de `SqlTypes` são NULL. A propriedade `IsNull` sempre retorna um valor true ou false.  
  
## <a name="precision"></a>Precisão  
 Tipos de dados decimais no CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] têm valores máximos diferentes em relação aos tipos de dados numéricos e decimais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Além disso, no CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], tipos de dados decimais supõem a precisão máxima. No CLR do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no entanto, `SqlDecimal` fornece a mesma precisão e escala máximas, além da mesma semântica do tipo de dados decimal do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="overflow-detection"></a>Detecção de estouro  
 No CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], a adição de dois números muito grandes pode não lançar uma exceção. Na verdade, caso nenhum operador de verificação tenha sido usado, o resultado retornado pode ser "delimitado" como um inteiro negativo. Em `System.Data.SqlTypes`, são lançadas exceções para todos os estouros e erros de estouro, além de erros de divisão por zero.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados do SQL Server no .NET Framework](sql-server-data-types-in-the-net-framework.md)  
  
  