---
title: Suporte a FOR XML para os UDTs (tipos de dados definidos pelo usuário) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- UDTs [SQL Server], XML
- user-defined types [SQL Server], XML
ms.assetid: 354e2150-fa2a-4583-b1aa-6b78ae4378b6
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 713b1bbf215f9f0748de647264697ca30e0d99da
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37242326"
---
# <a name="for-xml-support-for-the-user-defined-data-types-udt"></a>Suporte a FOR XML para os UDTs (tipos de dados definidos pelo usuário)
  FOR XML não oferece suporte a UDTs (tipos de dados definidos pelo usuário) do CLR (Common Language Runtime).  
  
 Para usar FOR XML com tipos definidos pelo usuário do CLR, verifique se o tipo de dados tem uma serialização XML e usa uma conversão explícita para XML na cláusula select de FOR XML.  
  
## <a name="see-also"></a>Consulte também  
 [Suporte a FOR XML para vários tipos de dados SQL Server](for-xml-support-for-various-sql-server-data-types.md)  
  
  
