---
title: Manipulando parâmetros de LOB (objeto grande) no CLR | Microsoft Docs
description: Este artigo descreve como lidar com valores de LOB (objeto grande) para parâmetros em SQL Server integração CLR. Use SqlBytes e SqlChars para tipos LOB.
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
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
ms.openlocfilehash: 0b10ac8c1ac9ccba804b892617df0b8d6c0d2f14
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85637487"
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>Manipulando parâmetros de LOB (objeto grande) no CLR
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use **SqlBytes** e **SqlChars** para passar o tipo binário de LOB (objeto grande) (**varbinary (max)**) e os parâmetros de tipo de caractere LOB (**nvarchar (max)**), respectivamente. Estes tipos permitem o fluxo contínuo de valores LOB do banco de dados para a rotina CLR (common language runtime), em vez de copiar todo o valor para o espaço gerenciado. **SqlBinary** e **SqlString** devem ser usados apenas para valores pequenos de cadeia de caracteres e binários.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados do SQL Server no .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
