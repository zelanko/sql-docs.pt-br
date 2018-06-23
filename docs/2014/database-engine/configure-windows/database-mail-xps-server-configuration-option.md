---
title: Opção de configuração de servidor Database Mail XPs | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Database Mail XPs option
- Database Mail [SQL Server], enabling
ms.assetid: e22c4e63-1792-473b-af11-14a7931ca9ed
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7aeecaabec0c476768e7e98579086e7f36649abc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019878"
---
# <a name="database-mail-xps-server-configuration-option"></a>Opção de configuração de servidor Database Mail XPs
  Use a opção **DatabaseMail XPs** para habilitar o Database Mail neste servidor. Os valores possíveis são:  
  
-   **0** , indicando que o Database Mail não está disponível (padrão).  
  
-   **1** , indicando que o Database Mail está disponível.  
  
 A configuração entra em vigor imediatamente, sem que o servidor seja parado e reiniciado.  
  
 Depois de habilitar o Database Mail, você deve configurar um banco de dados de host de Database Mail para usar o Database Mail.  
  
 Configurar o Database Mail por meio do **Assistente para Configuração do Database Mail** faz com que sejam habilitados os procedimentos armazenados estendidos do Database Mail no banco de dados **msdb** . Se usar o **Assistente para Configuração do Database Mail**, você não precisará usar o exemplo de **sp_configure** abaixo.  
  
 Definir a opção **Database Mail XPs** como 0 impede que o Database Mail seja iniciado. Se estiver em execução quando a opção for definida como 0, ele continuará em execução e enviando emails até estar ocioso pelo tempo configurado na opção **DatabaseMailExeMinimumLifeTime** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir habilita os procedimentos armazenados estendidos do Database Mail.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Database Mail XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)  
  
  