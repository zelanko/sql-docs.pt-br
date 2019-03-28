---
title: Suporte a FOR XML para os UDTs (tipos de dados definidos pelo usuário) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- UDTs [SQL Server], XML
- user-defined types [SQL Server], XML
ms.assetid: 354e2150-fa2a-4583-b1aa-6b78ae4378b6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6e41f5a97c4b32611589e5da24a95e237416a5b2
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533958"
---
# <a name="for-xml-support-for-the-user-defined-data-types-udt"></a>Suporte a FOR XML para os UDTs (tipos de dados definidos pelo usuário)
  FOR XML não oferece suporte a UDTs (tipos de dados definidos pelo usuário) do CLR (Common Language Runtime).  
  
 Para usar FOR XML com tipos definidos pelo usuário do CLR, verifique se o tipo de dados tem uma serialização XML e usa uma conversão explícita para XML na cláusula select de FOR XML.  
  
## <a name="see-also"></a>Consulte também  
 [Suporte a FOR XML para vários tipos de dados SQL Server](for-xml-support-for-various-sql-server-data-types.md)  
  
  
