---
title: "Configurar alertas para notificar os administradores de políticas sobre falhas | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, configure alerts
ms.assetid: e8e60159-d5b0-49d5-91f3-af8e9cb994c1
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 44565d371ca75d4d707274b90d52794473f63a72
ms.lasthandoff: 04/11/2017

---
# <a name="configure-alerts-to-notify-policy-administrators-of-policy-failures"></a>Configurar alertas para notificar os administradores de políticas sobre falhas
  Quando as políticas do Gerenciamento Baseado em Políticas são executadas em um dos três modos de avaliação automatizados, se ocorrer uma violação de política, uma mensagem será gravada no log de eventos. Para ser notificado quando essa mensagem for gravada no log de eventos, você pode criar um alerta para detectar a mensagem e executar uma ação. O alerta deve detectar as mensagens como mostra a tabela a seguir.  
  
|Modo de execução|Número da mensagem|  
|--------------------|--------------------|  
|Ao alterar: impedir<br /><br /> (se automático)|34050|  
|Ao alterar: impedir<br /><br /> (se por demanda)|34051|  
|Ao agendar|34052|  
|Ao alterar|34053|  
  
 Para configurar um alerta para responder às mensagens de erro do Gerenciamento Baseado em Políticas, consulte os seguintes tópicos:  
  
-   [Criar um operador](http://msdn.microsoft.com/library/1359d790-5905-4927-a208-e7155e7768a2)  
  
-   [Criar um alerta usando um número de erro](http://msdn.microsoft.com/library/03dd7fac-5073-4f86-babd-37e45a86023c)  
  
-   [Atribuir alertas a um operador](http://msdn.microsoft.com/library/aa818155-6fa2-4565-a09f-5c7e31c89754)  
  
## <a name="permissions"></a>Permissões  
 Quando as políticas são avaliadas por demanda, elas são executadas no contexto de segurança do usuário. Para gravar no log de erros, o usuário deve ter permissões ALTER TRACE ou ser um membro da função de servidor fixa sysadmin. As políticas avaliadas por um usuário que tenha menos privilégios não são gravadas no log de eventos e não disparam um alerta.  
  
 Os modos de execução automatizados são executados como um membro da função sysadmin. Isso permite que a política grave no log de erros e gere um alerta.  
  
## <a name="additional-considerations-about-alerts"></a>Considerações adicionais sobre alertas  
 Esteja atento às seguintes considerações adicionais sobre alertas:  
  
-   Os alertas só são gerados para políticas que estiverem habilitadas. Como as políticas **Sob demanda** não podem ser habilitadas, não são gerados alertas para políticas executadas sob demanda.  
  
-   Se a ação que você deseja executar incluir o envio de um email, você deverá configurar uma conta de email. É recomendável usar o Database Mail. Para obter mais informações sobre como configurar o Database Mail, veja [Criar uma conta do Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md).  
  
  
