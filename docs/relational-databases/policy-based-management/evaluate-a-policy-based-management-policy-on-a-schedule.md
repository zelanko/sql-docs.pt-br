---
description: Avaliar uma política do Gerenciamento Baseado em Políticas em um agendamento
title: Avaliar uma política do gerenciamento baseado em políticas em um agendamento | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: bea09522-ff47-4037-ab55-a98ea7c10099
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 79e16f9a39e235f7ceed5a77e55d03f4c5efed72
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127877"
---
# <a name="evaluate-a-policy-based-management-policy-on-a-schedule"></a>Avaliar uma política do Gerenciamento Baseado em Políticas em um agendamento
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como avaliar uma faceta do Gerenciamento Baseado em Políticas em um agendamento no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para avaliar uma política em um agendamento, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-evaluate-a-policy-on-a-schedule"></a>Para avaliar uma política em um agendamento  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém o agendamento da política que você deseja avaliar.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Gerenciamento de Política**.  
  
4.  Clique no sinal de adição para expandir a pasta **Políticas** .  
  
5.  Clique com o botão direito do mouse na política cujo agendamento você deseja avaliar e selecione **Propriedades**.  
  
6.  Na caixa de diálogo **Abrir Política -** _nome_da_política_, na lista **Modo de Avaliação**, selecione **Ao agendar**.  
  
7.  Em **Agenda**, clique em **Escolher** para especificar uma agenda existente ou em **Novo** para criar uma agenda nova.  
  
8.  Quando terminar, clique em **OK**.  
  
  
