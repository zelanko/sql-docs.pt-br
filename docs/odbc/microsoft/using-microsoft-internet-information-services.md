---
title: "Usando os serviços de informações da Internet da Microsoft | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], IIS
- internet information services [ODBC]
- IIS [ODBC]
ms.assetid: 3328f2f1-b34a-472f-82cf-ad49768ff061
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8d3fafae5326b9631965ffdf7714b4de781cc5fa
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="using-microsoft-internet-information-services"></a>Usando os serviços de informações da Internet da Microsoft
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Se você tiver dificuldade para se conectar de dentro de um script do IIS (especialmente se você receber um erro ORA-12641), adicione a seguinte linha ao arquivo SQLNET:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 Isso irá desabilitar os serviços de rede seguro para que possa se conectar usando a autenticação anônima.
