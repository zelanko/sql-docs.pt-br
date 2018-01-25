---
title: "Opção de configuração do servidor server trigger recursion | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- recursive triggers [SQL Server]
- triggers [SQL Server], recursive
- server trigger recursion option
ms.assetid: da4c25f5-d04c-4951-a3db-409e71a1b468
caps.latest.revision: "24"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f22eab2dd49dc6d77d67e0ad4f4baf9d63769fa6
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="server-trigger-recursion-server-configuration-option"></a>Opção de configuração de servidor server trigger recursion
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use a opção **server trigger recursion** para especificar se os gatilhos de nível de servidor podem ser acionados recursivamente. Quando esta opção for definida como 1 (ON), será permitido que os gatilhos de nível de servidor sejam acionados recursivamente. Quando ela for definida como 0 (OFF), os gatilhos de nível de servidor não poderão ser acionados recursivamente. Somente a recursão direta é evitada quando a opção server trigger recursion é definida como 0 (OFF). (Para desabilitar a recursão indireta, defina a opção **nested triggers** como 0.) O valor padrão desta opção é 1 (ON). A configuração entra em vigor imediatamente (sem a reinicialização do servidor).  
  
 Para obter mais informações, consulte [Criar gatilhos aninhados](../../relational-databases/triggers/create-nested-triggers.md).  
  
## <a name="see-also"></a>Consulte Também  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
