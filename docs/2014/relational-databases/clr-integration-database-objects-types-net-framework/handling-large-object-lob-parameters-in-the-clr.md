---
title: Parâmetros de objeto grande (LOB) no CLR tratamento | Microsoft Docs
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
- large data, CLR integration
- LOB data [SQL Server], CLR integration
- SqlBytes data type
- SqlChars data type
ms.assetid: d07956f6-9543-4476-9426-536f95991150
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 58b2e188a69799dd0b8d36958a7059d5cfcc09f9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120591"
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>Manipulando parâmetros de LOB (objeto grande) no CLR
  Use `SqlBytes` e `SqlChars` para passar parâmetros dos tipos objeto grande binário (LOB) (`varbinary(max)`) e caractere LOB (`nvarchar(max)`), respectivamente. Estes tipos permitem o fluxo contínuo de valores LOB do banco de dados para a rotina CLR (common language runtime), em vez de copiar todo o valor para o espaço gerenciado. `SqlBinary` e `SqlString` devem ser usados somente para valores baixos de cadeia de caracteres e binários.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados do SQL Server no .NET Framework](sql-server-data-types-in-the-net-framework.md)  
  
  