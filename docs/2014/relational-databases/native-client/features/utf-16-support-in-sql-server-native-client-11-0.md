---
title: Suporte a UTF-16 no SQL Server Native Client 11,0 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b28d869a6e33969550751158e321ec24062bf6ac
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707153"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>Suporte a UTF-16 no SQL Server Native Client 11.0
  A partir do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] , se você fornecer um buffer de comprimento fixo ao associar um resultado de coluna ou um parâmetro de saída e se o `wchar` caractere gravado no buffer antes do caractere de terminação for um ponto de código substituto alto de um par substituto, e se o próximo `wchar` caractere for um ponto de código substituto baixo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Native Client não adicionará o ponto de código substituto alto ao buffer.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do SQL Server Native Client](sql-server-native-client-features.md)  
  
  
