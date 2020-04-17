---
title: Nulidade e Comparações lógicas de três valores | Microsoft Docs
description: Este artigo abrange como os tipos de dados do SQL Server diferem dos tipos em System.Data.SqlTypes no Framework .NET, que têm semântica e precisão semelhantes.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- precision [CLR integration]
- overflow detections [CLR integration]
- null values [CLR integration]
- three-value logic comparisons [CLR integration]
- data types [CLR integration]
- SqlBoolean data type
ms.assetid: 13da4c7f-1010-4b2d-a63c-c69b6bfd96f1
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f016abf2113afef3e02f01fd9842b91b742d50a
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488431"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Comparações de lógica de três valores e nulidade
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Se você estiver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] familiarizado com os tipos de dados, você encontrará semântica e precisão [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]semelhantes no espaço de nome **System.Data.SqlTypes** no . No entanto, há algumas diferenças, e este tópico aborda a mais importante delas.  
  
## <a name="null-values"></a>Valores NULL  
 A principal diferença entre os tipos de dados CLR (Common Language Runtime) nativos e os tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é que os primeiros não permitem valores NULL, ao passo que os últimos fornecem uma semântica NULL completa.  
  
 As comparações são afetadas por valores NULL. Durante a comparação entre dois valores x e y, caso x ou y seja NULL, algumas comparações lógicas são avaliadas como UNKNOWN, e não como true ou false.  
  
## <a name="sqlboolean-data-type"></a>Tipo de dados SqlBoolean  
 O **namespace System.Data.SqlTypes** introduz um tipo **SqlBoolean** para representar essa lógica de 3 valores. Comparações entre qualquer **SqlTypes** retornam um tipo de valor **SqlBoolean.** O valor DESCONHECIDO é representado pelo valor nulo do tipo **SqlBoolean.** As propriedades **IsTrue**, **IsFalse**e **IsNull** são fornecidas para verificar o valor de um tipo **SqlBoolean.**  
  
## <a name="operations-functions-and-null-values"></a>Operações, funções e valores NULL  
 Todos os operadores aritméticos \*(+, -, , /, %), operadores bitwise (~, & e |), e a maioria das funções retornam NULL se qualquer um dos operands ou argumentos de **SqlTypes** são NULAS. A propriedade **IsNull** sempre retorna um valor verdadeiro ou falso.  
  
## <a name="precision"></a>Precisão  
 Tipos de dados decimais no CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] têm valores máximos diferentes em relação aos tipos de dados numéricos e decimais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Além disso, no CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], tipos de dados decimais supõem a precisão máxima. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]entanto, o **SqlDecimal** fornece a mesma precisão e escala máxima semântica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de dados decimais em .  
  
## <a name="overflow-detection"></a>Detecção de estouro  
 No CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], a adição de dois números muito grandes pode não lançar uma exceção. Na verdade, caso nenhum operador de verificação tenha sido usado, o resultado retornado pode ser "delimitado" como um inteiro negativo. Em **System.Data.SqlTypes**, as exceções são lançadas para todos os erros de estouro e subfluxo e erros divididos por zero.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados do SQL Server no .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
