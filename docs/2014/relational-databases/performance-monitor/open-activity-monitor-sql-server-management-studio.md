---
title: Abrir o Monitor de Atividade (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Activity Monitor [SQL Server], setting the refresh interval
- refresh interval for Activity Monitor
- Activity Monitor [SQL Server], opening
- opening Activity Monitor
ms.assetid: 0a6eeb16-f02b-479d-9a60-543e40ebf46b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0d1c0312acfcd2e5dbb17d740fe2659cb8c91bbe
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63032000"
---
# <a name="open-activity-monitor-sql-server-management-studio"></a>Abrir o Monitor de Atividade (SQL Server Management Studio)
  Este tópico descreve como abrir o Monitor de Atividade para obter informações sobre os processos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e como esses processos afetam a instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Descreve também como definir o intervalo de atualização do Monitor de Atividade.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para abrir o Monitor de Atividade usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
-   **Para definir o intervalo de atualização usando:**  [SQL Server Management Studio](#Refresh)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
 O Monitor de Atividade executa consultas na instância monitorada a fim de obter informações para os painéis de exibição do Monitor de Atividade. Quando o intervalo de atualização for definido para menos de 10 segundos, o tempo usado para executar essas consultas poderá afetar o desempenho do servidor.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Para exibir o Monitor de Atividade, um usuário deve ter a permissão VIEW SERVER STATE. Para exibir a seção E/S de Arquivo de Dados do Monitor de Atividade, você deve ter a permissão CREATE DATABASE, ALTER ANY DATABASE ou VIEW ANY DEFINITION além da permissão VIEW SERVER STATE.  
  
 Para executar KILL em um processo, o usuário deve ser um membro das funções de servidor fixas sysadmin ou processadmin.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-open-activity-monitor-in-sql-server-management-studio"></a>Para abrir o Monitor de Atividade no SQL Server Management Studio  
  
1.  Na barra de ferramentas padrão do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , clique em **Monitor de Atividade**.  
  
2.  Na caixa de diálogo **Conectar ao Servidor** , selecione o nome do servidor e o modo de autenticação e clique em **Conectar**.  
  
 Também é possível abrir o Monitor de Atividade a qualquer momento pressionando CTRL+ALT A.  
  
#### <a name="to-open-activity-monitor-in-object-explorer"></a>Para abrir o Monitor de Atividade no Pesquisador de Objetos  
  
-   No Pesquisador de objetos, clique com o botão direito do mouse no nome da instância e selecione **Monitor de atividade**.  
  
#### <a name="to-open-activity-monitor-when-opening-sql-server-management-studio"></a>Para abrir o Monitor de Atividade ao abrir o SQL Server Management Studio  
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  Na caixa de diálogo **Opções** , expanda **Ambiente**e, em seguida, selecione **Geral**.  
  
3.  Na caixa **Na inicialização** , selecione **Abrir Pesquisador de Objetos e Monitor de Atividade**.  
  
4.  Para ativar as alterações, feche e reabra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
###  <a name="to-set-the-activity-monitor-refresh-interval"></a><a name="Refresh"></a>Para definir o intervalo de atualização do monitor de atividade  
  
-   Abra o Monitor de Atividade.  
  
-   Clique com o botão direito do mouse em **Visão Geral**, selecione **Intervalo de Atualização**e selecione o intervalo em que o Monitor de Atividade deve obter novas informações sobre a instância.  
  
  
