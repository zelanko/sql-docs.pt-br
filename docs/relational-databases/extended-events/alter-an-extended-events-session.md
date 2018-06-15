---
title: Alterar uma sessão eventos estendidos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 114ec05b-7eca-4c87-b276-25e37b84be39
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 614b322beaf2c8e9e7c818341983f58a6228debf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32935496"
---
# <a name="alter-an-extended-events-session"></a>Alterar uma sessão de Eventos Estendidos
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Depois que você criar uma sessão de Eventos Estendidos, poderá alterá-la de acordo com suas necessidades usando o **Assistente de Eventos Estendidos do SQL Server**.  
  
## <a name="before-you-begin"></a>Antes de começar  
 Não é possível alterar um destino para sessões ativas e inativas e nem as configurações de propriedades avançadas de uma sessão ativa.  
  
 Você pode fazer as seguintes alterações em sessões de evento ativas e inativas:  
  
-   Adicione ou remova eventos da sessão e altere as configurações de evento, como campos de evento, filtros e ações.  
  
-   Adicione ou remova um destino da sessão de evento.  
  
-   Habilite a opção **Iniciar a sessão de evento na inicialização do servidor** .  
  
 Você pode fazer as seguintes alterações adicionais em uma sessão de evento inativa:  
  
-   Habilite a opção **Rastrear a relação entre eventos** .  
  
-   Altere a configuração das propriedades avançadas.  
  
> [!NOTE]  
>  O **Assistente de Eventos Estendidos do SQL Server** não dá suporte à modificação da sessão de eventos.  
  
## <a name="how-to-alter-an-extended-events-session-using-the-sql-server-extended-events-wizard"></a>Como alterar uma sessão de Eventos Estendidos usando o Assistente de Eventos Estendidos do SQL Server  
  
-   No Pesquisador de Objetos, expanda **Gerenciamento**, expanda **Eventos Estendidos**e, em seguida, expanda **Sessões**.  
  
-   Clique com o botão direito do mouse na sessão a ser alterada e clique em **Propriedades**.  
  
-   Na caixa de diálogo **Propriedades** , faça as alterações apropriadas e clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [Criar uma sessão de Eventos Estendidos usando o Editor de Consultas](http://msdn.microsoft.com/library/cba0e02b-b201-4863-bf1b-9164e68e5fa8)  
  
  
