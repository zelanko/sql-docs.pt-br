---
title: Usando serviços de informações da Microsoft na Internet | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], IIS
- internet information services [ODBC]
- IIS [ODBC]
ms.assetid: 3328f2f1-b34a-472f-82cf-ad49768ff061
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c71babf933c2615e6c2464696c1023ccaf53dd7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282457"
---
# <a name="using-microsoft-internet-information-services"></a>Usar os Serviços de Informações da Internet da Microsoft
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Se você tiver dificuldade em se conectar dentro de um script IIS (particularmente se você receber um erro ORA-12641), adicione a seguinte linha ao arquivo Sqlnet.ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 Isso desativará os Serviços de Rede Segura para que você possa se conectar usando autenticação anônima.
