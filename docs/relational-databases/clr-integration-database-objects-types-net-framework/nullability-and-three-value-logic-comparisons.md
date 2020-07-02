---
title: Comparações de lógica de três valores e nulidade | Microsoft Docs
description: Este artigo aborda como SQL Server tipos de dados diferem dos tipos em System. Data. SqlTypes no .NET Framework, que têm semântica e precisão semelhantes.
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
ms.openlocfilehash: 2c81ba685de223f213da150da0edb930385b84d5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85719923"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Comparações de lógica de três valores e nulidade
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Se você estiver familiarizado com os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados, encontrará semântica e precisão semelhantes no namespace **System. Data. SqlTypes** no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . No entanto, há algumas diferenças, e este tópico aborda a mais importante delas.  
  
## <a name="null-values"></a>Valores NULL  
 A principal diferença entre os tipos de dados CLR (Common Language Runtime) nativos e os tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é que os primeiros não permitem valores NULL, ao passo que os últimos fornecem uma semântica NULL completa.  
  
 As comparações são afetadas por valores NULL. Durante a comparação entre dois valores x e y, caso x ou y seja NULL, algumas comparações lógicas são avaliadas como UNKNOWN, e não como true ou false.  
  
## <a name="sqlboolean-data-type"></a>Tipo de dados SqlBoolean  
 O namespace **System. Data. SqlTypes** introduz um tipo **SqlBoolean** para representar essa lógica de 3 valores. As comparações entre qualquer **SqlType** retornam um tipo de valor **SqlBoolean** . O valor desconhecido é representado pelo valor nulo do tipo **SqlBoolean** . As propriedades **IsTrue**, **IsFalse**e **IsNull** são fornecidas para verificar o valor de um tipo **SqlBoolean** .  
  
## <a name="operations-functions-and-null-values"></a>Operações, funções e valores NULL  
 Todos os operadores aritméticos (+,-, \* ,/,%), operadores de bit (~, & e |) e a maioria das funções retornarão NULL se qualquer um dos operandos ou argumentos de **SqlTypes** forem nulos. A propriedade **IsNull** sempre retorna um valor verdadeiro ou falso.  
  
## <a name="precision"></a>Precisão  
 Tipos de dados decimais no CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] têm valores máximos diferentes em relação aos tipos de dados numéricos e decimais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Além disso, no CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], tipos de dados decimais supõem a precisão máxima. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entanto, no CLR para, **SqlDecimal** fornece a mesma precisão e escala máximas e a mesma semântica que o tipo de dados decimal no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="overflow-detection"></a>Detecção de estouro  
 No CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], a adição de dois números muito grandes pode não lançar uma exceção. Na verdade, caso nenhum operador de verificação tenha sido usado, o resultado retornado pode ser "delimitado" como um inteiro negativo. Em **System. Data. SqlTypes**, as exceções são geradas para todos os erros de estouro e Subfluxo e erros de divisão por zero.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados do SQL Server no .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
