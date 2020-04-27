---
title: Suporte a UTF-16 no SQL Server Native Client 11,0 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 415cb2fe8a3295770cfc8bd2d5c6e56750adb6d9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63205117"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>Suporte a UTF-16 no SQL Server Native Client 11.0
  A partir [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]do, se você fornecer um buffer de comprimento fixo ao associar um resultado de coluna ou um parâmetro de `wchar` saída e se o caractere gravado no buffer antes do caractere de terminação for um ponto de código substituto alto de um par `wchar` substituto, e se o próximo caractere for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] um ponto de código substituto baixo, o Native Client não adicionará o ponto de código substituto alto ao buffer.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do SQL Server Native Client](sql-server-native-client-features.md)  
  
  
