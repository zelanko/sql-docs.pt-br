---
title: Alterar uma sessão de Eventos Estendidos
description: Use o assistente de Eventos Estendidos do SQL Server para alterar uma sessão de Eventos Estendidos. As alterações que você pode fazer dependem de se a sessão está ativa ou inativa.
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: 114ec05b-7eca-4c87-b276-25e37b84be39
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 26c54a8100f697275e87826e949f8b83276507a5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85778456"
---
# <a name="alter-an-extended-events-session"></a>Alterar uma sessão de Eventos Estendidos

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

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
 [Criar uma sessão de Eventos Estendidos usando o Editor de Consultas](quick-start-extended-events-in-sql-server.md)  
  
  
