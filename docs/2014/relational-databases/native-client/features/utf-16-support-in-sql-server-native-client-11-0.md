---
title: Suporte a UTF-16 no SQL Server Native Client 11.0 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 66198f42676944967a2d655f14a27470922fd318
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119328"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>Suporte a UTF-16 no SQL Server Native Client 11.0
  A partir do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], se você fornecer um buffer de comprimento fixo ao associar um coluna de resultados ou parâmetro de saída e se o `wchar` caractere gravado no buffer antes da finalização do caractere é um ponto de código alternativo alto de um par substituto e se o próximo `wchar` caractere é um ponto de código alternativo baixo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client não adicionará o ponto de código alternativo alto ao buffer.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do SQL Server Native Client](sql-server-native-client-features.md)  
  
  