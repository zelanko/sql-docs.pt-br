---
title: Comparações de lógica de três valores e nulidade | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: e29b2ad4c4049890bef1ee319d37847a0e21cacd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47676136"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Comparações de lógica de três valores e nulidade
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Se você estiver familiarizado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados, você encontrará semântica e precisão em semelhantes a **SqlTypes** namespace no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. No entanto, há algumas diferenças, e este tópico aborda a mais importante delas.  
  
## <a name="null-values"></a>Valores NULL  
 A principal diferença entre os tipos de dados CLR (Common Language Runtime) nativos e os tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é que os primeiros não permitem valores NULL, ao passo que os últimos fornecem uma semântica NULL completa.  
  
 As comparações são afetadas por valores NULL. Durante a comparação entre dois valores x e y, caso x ou y seja NULL, algumas comparações lógicas são avaliadas como UNKNOWN, e não como true ou false.  
  
## <a name="sqlboolean-data-type"></a>Tipo de dados SqlBoolean  
 O **SqlTypes** namespace introduz uma **SqlBoolean** tipo para representar essa lógica de valor de 3. Comparações entre qualquer **SqlTypes** retornar uma **SqlBoolean** tipo de valor. O valor desconhecido é representado pelo valor nulo a **SqlBoolean** tipo. As propriedades **IsTrue**, **IsFalse**, e **IsNull** são fornecidos para verificar o valor de uma **SqlBoolean** tipo.  
  
## <a name="operations-functions-and-null-values"></a>Operações, funções e valores NULL  
 Todos os operadores aritméticos (+, -, \*, /, %), operadores bit a bit (~, &, e |), e a maioria das funções retornarão NULL se qualquer um dos operandos ou argumentos de **SqlTypes** forem NULL. O **IsNull** propriedade sempre retorna um valor true ou false.  
  
## <a name="precision"></a>Precisão  
 Tipos de dados decimais no CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] têm valores máximos diferentes em relação aos tipos de dados numéricos e decimais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Além disso, no CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], tipos de dados decimais supõem a precisão máxima. No CLR do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no entanto, **SqlDecimal** fornece a mesma precisão máxima e a escala e a mesma semântica que o tipo de dados decimais no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="overflow-detection"></a>Detecção de estouro  
 No CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], a adição de dois números muito grandes pode não lançar uma exceção. Na verdade, caso nenhum operador de verificação tenha sido usado, o resultado retornado pode ser "delimitado" como um inteiro negativo. Na **SqlTypes**, as exceções são geradas para todos os erros de divisão por zero e erros de estouro negativo e estouro.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados do SQL Server no .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
