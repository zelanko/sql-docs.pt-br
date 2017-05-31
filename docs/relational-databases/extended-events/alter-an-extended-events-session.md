---
title: "Alterar uma sessão eventos estendidos | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
- xevents
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 114ec05b-7eca-4c87-b276-25e37b84be39
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9330ef01cb491fef9307149e0cc774fa2b042c52
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="alter-an-extended-events-session"></a>Alterar uma sessão de Eventos Estendidos
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

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
  
## <a name="see-also"></a>Consulte também  
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [Criar uma sessão de Eventos Estendidos usando o Editor de Consultas](http://msdn.microsoft.com/library/cba0e02b-b201-4863-bf1b-9164e68e5fa8)  
  
  
