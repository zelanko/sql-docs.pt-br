---
title: Configurar o SQL Server Agent Mail para usar o Database Mail | Microsoft Docs
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], SQL Server Agent Mail
- SQL Server Agent Mail
ms.assetid: 4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e4c762c16a15b4e6cee20598f87c5a9ca9955eac
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51559893"
---
# <a name="configure-sql-server-agent-mail-to-use-database-mail"></a>Configurar o SQL Server Agent Mail para usar o Database Mail
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para usar o Database Mail para enviar notificação e alertas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  Para obter informações sobre como habilitar e configurar o Database Mail, consulte [Configurar o Database Mail](../../relational-databases/database-mail/configure-database-mail.md).  Para obter um exemplo de como usar o [!INCLUDE[tsql](../../includes/tsql-md.md)], consulte [Criar um perfil do Database Mail](../../relational-databases/database-mail/create-a-database-mail-profile.md).
  
-   **Antes de começar:**  
  
-   [Pré-requisitos](#Prerequisites)  
  
-   [Segurança](#Security)  
  
-   [Para configurar o SQL Server Agent para usar o Database Mail, usando o SQL Server Management Studio](#SSMSProcedure)  
  
-   [Tarefas de acompanhamento](#Follow_Up)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   [Habilite o Database Mail](../../relational-databases/database-mail/configure-database-mail.md).  
  
-    [Crie uma conta do Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md) para a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a ser usada.  
  
-   [Crie um perfil do Database Mail](../../relational-databases/database-mail/create-a-database-mail-profile.md) para a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a ser usada e adicione o usuário a **DatabaseMailUserRole** no banco de dados **msdb** .  
  
-   Defina o perfil como o perfil padrão para o banco de dados **msdb** .  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 O usuário que cria as contas de perfis e executa procedimentos armazenados deve ser membro da função de servidor fixa sysadmin.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para configurar o SQL Server Agent para usar o Database Mail**  
  
-   No Pesquisador de Objetos, expanda uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Clique com o botão direito do mouse em **SQL Server Agent**e então clique em **Propriedades**.  
  
-   Clique em **Sistema de Alerta**.  
  
-   Selecione **Habilitar Perfil de Email**.  
  
-   Na lista **Sistema de email** , selecione **Database Mail**.  
  
-   Na lista **Perfil de email**, selecione um perfil de email para o Database Mail.  
  
-   Reinicie o SQL Server Agent.  
  
##  <a name="Follow_Up"></a> Tarefas de acompanhamento  
 As tarefas a seguir são necessárias para concluir a configuração do Agent a fim de enviar alertas e notificações.  
  
-   [Alertas](../../ssms/agent/alerts.md)  
  
     Os alertas podem ser configurados para notificar um operador sobre um evento de banco de dados em particular ou uma condição do sistema operacional.  
  
-   [Operadores](../../ssms/agent/operators.md)  
  
     Os operadores são alias de pessoas ou grupos que podem receber notificação eletrônica.  
  
  
