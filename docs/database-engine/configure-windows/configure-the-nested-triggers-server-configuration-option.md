---
title: "Configurar a op&#231;&#227;o de configura&#231;&#227;o de servidor nested triggers | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "opção nested triggers"
ms.assetid: 29d7372b-d406-4a5b-80c6-a2d231d25211
caps.latest.revision: 27
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 27
---
# Configurar a op&#231;&#227;o de configura&#231;&#227;o de servidor nested triggers
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como configurar a opção de configuração de servidor **nested triggers** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção **nested triggers** controla se um gatilho AFTER pode ser colocado em cascata. Ou seja, executar uma ação que inicia outro gatilho que inicia outro gatilho e assim por diante. Quando **nested triggers** é definido como 0, os gatilhos AFTER não podem ser colocados em cascata. Quando **nested triggers** é definido como 1 (o padrão), os gatilhos AFTER podem ser colocados em cascata em até 32 níveis. Gatilhos INSTEAD OF podem ser aninhados, independentemente da configuração dessa opção.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção nested triggers usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção nested triggers](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### Para configurar a opção nested triggers  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Na página **Avançado**, defina a opção **Permitir que Gatilhos Disparem Outros Gatilhos** como **Verdadeiro** (o padrão) ou **Falso**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para configurar a opção nested triggers  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para definir o valor da opção `nested triggers` como `0`.  
  
```wmimof  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'nested triggers', 0 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Para obter mais informações, consulte [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de configurar a opção nested triggers  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## Consulte também  
 [Criar gatilhos aninhados](../../relational-databases/triggers/create-nested-triggers.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  