---
title: Opção de configuração do servidor server trigger recursion | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- recursive triggers [SQL Server]
- triggers [SQL Server], recursive
- server trigger recursion option
ms.assetid: da4c25f5-d04c-4951-a3db-409e71a1b468
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f1fc67db5d7d62c9257f6d66359b0166b6ed8c0b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62808877"
---
# <a name="server-trigger-recursion-server-configuration-option"></a>Opção de configuração de servidor server trigger recursion
  Use a opção **server trigger recursion** para especificar se os gatilhos de nível de servidor podem ser acionados recursivamente. Quando esta opção for definida como 1 (ON), será permitido que os gatilhos de nível de servidor sejam acionados recursivamente. Quando ela for definida como 0 (OFF), os gatilhos de nível de servidor não poderão ser acionados recursivamente. Somente a recursão direta é evitada quando a opção server trigger recursion é definida como 0 (OFF). (Para desabilitar a recursão indireta, defina a opção **nested triggers** como 0.) O valor padrão desta opção é 1 (ON). A configuração entra em vigor imediatamente (sem a reinicialização do servidor).  
  
 Para obter mais informações, consulte [Criar gatilhos aninhados](../../relational-databases/triggers/create-nested-triggers.md).  
  
## <a name="see-also"></a>Consulte Também  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
