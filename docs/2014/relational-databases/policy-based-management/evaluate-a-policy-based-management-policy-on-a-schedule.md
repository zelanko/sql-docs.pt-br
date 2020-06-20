---
title: Avaliar uma política do gerenciamento baseado em políticas em um agendamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: bea09522-ff47-4037-ab55-a98ea7c10099
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a39b00bdb22cce3a15c06366c504f62305ded1f9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85047797"
---
# <a name="evaluate-a-policy-based-management-policy-on-a-schedule"></a>Avaliar uma política do Gerenciamento Baseado em Políticas em um agendamento
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
  
  
