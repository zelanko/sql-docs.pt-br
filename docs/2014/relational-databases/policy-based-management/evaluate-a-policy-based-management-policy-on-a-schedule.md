---
title: Avaliar uma política do gerenciamento baseado em políticas em um agendamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: bea09522-ff47-4037-ab55-a98ea7c10099
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 56354766e7000bf5e7d7a1eb214da1be796ae82f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010658"
---
# <a name="evaluate-a-policy-based-management-policy-on-a-schedule"></a>Avaliar uma política do Gerenciamento Baseado em Políticas em um agendamento
  Este tópico descreve como avaliar uma faceta do Gerenciamento Baseado em Políticas em um agendamento no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para avaliar uma política em um agendamento, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-evaluate-a-policy-on-a-schedule"></a>Para avaliar uma política em um agendamento  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém o agendamento da política que você deseja avaliar.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Gerenciamento de Política**.  
  
4.  Clique no sinal de adição para expandir a pasta **Políticas** .  
  
5.  Clique com o botão direito do mouse na política cujo agendamento você deseja avaliar e selecione **Propriedades**.  
  
6.  Na caixa de diálogo **Abrir Política –***policy_name*, na lista **Modo de Avaliação**, selecione **Ao agendar**.  
  
7.  Em **Agenda**, clique em **Escolher** para especificar uma agenda existente ou em **Novo** para criar uma agenda nova.  
  
8.  Quando terminar, clique em **OK**.  
  
  