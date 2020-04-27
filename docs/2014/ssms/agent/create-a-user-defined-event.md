---
title: Criar um evento definido pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent alerts, user-defined events
- user-defined events [SQL Server]
- multiple language support [SQL Server], alerts
- languages [SQL Server], alerts
- severity levels [SQL Server]
- global considerations [SQL Server], alerts
- events [SQL Server], user-defined
- SQL Server Agent alerts, multiple-language environments
- alerts [SQL Server], user-defined events
- alerts [SQL Server], multiple-language environments
- custom events [SQL Server Agent]
- international considerations [SQL Server], alerts
ms.assetid: 03d71a35-97fa-4bba-aa9a-23ac9c9cf879
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5625e65b1da45e05002b540774f441f2deabd3f4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63260945"
---
# <a name="create-a-user-defined-event"></a>Criar um evento definido pelo usuário
  Você pode criar eventos definidos pelo usuário caso deseje monitorar eventos diferentes daqueles predefinidos pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você também pode atribuir um nível de severidade a cada evento definido pelo usuário.  
  
> [!NOTE]  
>  Ao usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selecione a opção **Gravar no log de eventos de aplicativo do Windows** para cada mensagem de evento definido pelo usuário, a fim de garantir que as mensagens sejam registradas. Por padrão, as mensagens definidas pelo usuário que tenham severidade abaixo de 19 não são enviadas ao log de aplicativos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows quando ocorrem. Portanto, as mensagens definidas pelo usuário que tenham severidade abaixo de 19 não disparam alertas do SQL Server Agent.  
  
 Os eventos definidos pelo usuário devem ter um número de mensagem exclusivo. Os números de mensagem de um evento definido pelo usuário devem ser maiores que 50.000. Você pode definir mensagens para o evento em múltiplos idiomas. No entanto, deve existir uma mensagem de erro em **En-US** para que possam ser adicionadas mensagens em outros idiomas.  
  
 Se você administra um ambiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] multilíngue, crie mensagens definidas pelo usuário em cada um dos idiomas com suporte. Por exemplo, se estiver criando uma nova mensagem de evento a ser usada em dois servidores, um em inglês e outro em alemão, use o mesmo número de mensagem e de severidade para ambos, mas atribua um idioma diferente a cada um.  
  
 As seguintes tarefas proporcionam informações sobre como criar eventos definidos pelo usuário e alertas em resposta a eles:  
  
 **Para criar um alerta com base em um número de mensagem**  
  
-   [SQL Server Management Studio](create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)  
  
 **Para criar um alerta com base em níveis de severidade**  
  
-   [SQL Server Management Studio](create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)  
  
 **Para definir uma resposta a um alerta**  
  
-   [SQL Server Management Studio](../sql-server-management-studio-ssms.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql)  
  
 **Para criar uma mensagem de erro de evento definida pelo usuário**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addmessage-transact-sql)  
  
 **Para modificar uma mensagem de erro de evento definida pelo usuário**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-altermessage-transact-sql)  
  
 **Para excluir uma mensagem de erro de evento definida pelo usuário**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-dropmessage-transact-sql)  
  
 **Para desabilitar ou reativar um alerta**  
  
-   [SQL Server Management Studio](disable-or-reactivate-an-alert.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-alert-transact-sql)  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_update_alert](/sql/relational-databases/system-stored-procedures/sp-update-alert-transact-sql)  
  
  
