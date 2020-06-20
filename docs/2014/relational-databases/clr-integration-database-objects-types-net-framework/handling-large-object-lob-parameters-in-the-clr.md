---
title: Manipulando parâmetros de LOB (objeto grande) no CLR | Microsoft Docs
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
ms.openlocfilehash: ee791c73a6610761c2086723f9e41c2351b37dd0
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954746"
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>Manipulando parâmetros de LOB (objeto grande) no CLR
  Use `SqlBytes` e `SqlChars` para passar parâmetros dos tipos objeto grande binário (LOB) (`varbinary(max)`) e caractere LOB (`nvarchar(max)`), respectivamente. Estes tipos permitem o fluxo contínuo de valores LOB do banco de dados para a rotina CLR (common language runtime), em vez de copiar todo o valor para o espaço gerenciado. `SqlBinary` e `SqlString` devem ser usados somente para valores baixos de cadeia de caracteres e binários.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados do SQL Server no .NET Framework](sql-server-data-types-in-the-net-framework.md)  
  
  
