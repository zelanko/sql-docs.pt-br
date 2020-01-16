---
title: Suporte para FOR XML para UDT (tipos de dados definidos pelo usuário) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- UDTs [SQL Server], XML
- user-defined types [SQL Server], XML
ms.assetid: 354e2150-fa2a-4583-b1aa-6b78ae4378b6
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: 34764dcdc6b8f0fa91ce4a79ef6dde8cb8eaacc1
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244778"
---
# <a name="for-xml-support-for-the-user-defined-data-types-udt"></a>Suporte a FOR XML para os UDTs (tipos de dados definidos pelo usuário)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  FOR XML não oferece suporte a UDTs (tipos de dados definidos pelo usuário) do CLR (Common Language Runtime).  
  
 Para usar FOR XML com tipos definidos pelo usuário do CLR, verifique se o tipo de dados tem uma serialização XML e usa uma conversão explícita para XML na cláusula select de FOR XML.  
  
## <a name="see-also"></a>Consulte Também  
 [Suporte a FOR XML para vários tipos de dados de SQL Server](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
