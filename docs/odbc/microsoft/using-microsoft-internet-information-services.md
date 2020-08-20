---
description: Usar os Serviços de Informações da Internet da Microsoft
title: Usando o Microsoft Serviços de Informações da Internet | Microsoft Docs
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
ms.openlocfilehash: 5e20a15aad4409f535d83e813fdfbd911ca80674
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471328"
---
# <a name="using-microsoft-internet-information-services"></a>Usar os Serviços de Informações da Internet da Microsoft
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Se você tiver dificuldade para se conectar de dentro de um script do IIS (especialmente se você receber um erro ORA-12641), adicione a seguinte linha ao arquivo sqlnet. Ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 Isso desabilitará os serviços de rede segura para que você possa se conectar usando a autenticação anônima.
