---
title: Usando os serviços de informações da Internet da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], IIS
- internet information services [ODBC]
- IIS [ODBC]
ms.assetid: 3328f2f1-b34a-472f-82cf-ad49768ff061
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09aa384d3b5cd3f67d6bf6b75615bbf9047dff35
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="using-microsoft-internet-information-services"></a>Usando os serviços de informações da Internet da Microsoft
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Se você tiver dificuldade para se conectar de dentro de um script do IIS (especialmente se você receber um erro ORA-12641), adicione a seguinte linha ao arquivo SQLNET:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 Isso irá desabilitar os serviços de rede seguro para que possa se conectar usando a autenticação anônima.
