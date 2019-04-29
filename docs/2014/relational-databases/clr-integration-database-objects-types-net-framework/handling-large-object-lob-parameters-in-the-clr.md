---
title: Manipulando parâmetros de objeto grande (LOB) no CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- large data, CLR integration
- LOB data [SQL Server], CLR integration
- SqlBytes data type
- SqlChars data type
ms.assetid: d07956f6-9543-4476-9426-536f95991150
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 09797eac229a4b3b92f94a60b6e1c06c9ec12f08
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62919500"
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>Manipulando parâmetros de LOB (objeto grande) no CLR
  Use `SqlBytes` e `SqlChars` para passar parâmetros dos tipos objeto grande binário (LOB) (`varbinary(max)`) e caractere LOB (`nvarchar(max)`), respectivamente. Estes tipos permitem o fluxo contínuo de valores LOB do banco de dados para a rotina CLR (common language runtime), em vez de copiar todo o valor para o espaço gerenciado. `SqlBinary` e `SqlString` devem ser usados somente para valores baixos de cadeia de caracteres e binários.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados do SQL Server no .NET Framework](sql-server-data-types-in-the-net-framework.md)  
  
  
