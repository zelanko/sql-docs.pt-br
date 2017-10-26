---
title: "Opção de configuração de servidor Database Mail XPs | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Database Mail XPs option
- Database Mail [SQL Server], enabling
ms.assetid: e22c4e63-1792-473b-af11-14a7931ca9ed
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 989df51eeeb19f45e1c515637cce16783e5227a1
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="database-mail-xps-server-configuration-option"></a>Opção de configuração de servidor Database Mail XPs
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
  

