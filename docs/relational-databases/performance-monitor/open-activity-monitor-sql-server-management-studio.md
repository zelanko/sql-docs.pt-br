---
title: Abrir o Monitor de Atividade (SQL Server Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Activity Monitor [SQL Server], setting the refresh interval
- refresh interval for Activity Monitor
- Activity Monitor [SQL Server], opening
- opening Activity Monitor
ms.assetid: 0a6eeb16-f02b-479d-9a60-543e40ebf46b
caps.latest.revision: 38
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 45e63d53b65730136bbc0a4f20ad5d4215020c58
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="open-activity-monitor-sql-server-management-studio"></a>Abrir o Monitor de Atividade (SQL Server Management Studio)

   
 O Monitor de Atividade executa consultas na instância monitorada a fim de obter informações para os painéis de exibição do Monitor de Atividade. Quando o intervalo de atualização for definido para menos de 10 segundos, o tempo usado para executar essas consultas poderá afetar o desempenho do servidor.  
  
  
##  <a name="Permissions"></a> Verifique suas permissões.  
 Para exibir a atividade atual, é necessário ter a permissão VIEW SERVER STATE. Para exibir a seção E/S de Arquivo de Dados do Monitor de Atividade, você deve ter a permissão CREATE DATABASE, ALTER ANY DATABASE ou VIEW ANY DEFINITION além da permissão VIEW SERVER STATE.  
  
 Para executar KILL em um processo, o usuário deve ser um membro das funções de servidor fixas sysadmin ou processadmin.  
  
  
## <a name="open-activity-monitor"></a>Abrir o Monitor de Atividade  

### <a name="keyboard-shortcut"></a>Atalho de teclado  
 - Digite **CTRL+ALT+A** para abrir o Monitor de Atividade a qualquer momento.

 >**Dica!** Focalize o mouse em um ícone do SSMS para saber o que ele é e o atalho de teclado que ele ativa!

### <a name="toolbar"></a>Barra de Ferramentas

Na barra de ferramentas Padrão, clique no ícone **Monitor de Atividade** . Ele está no meio, logo à direita dos botões Desfazer/Refazer.
![Activity_Monitor_icon](../../relational-databases/performance-monitor/media/activity-monitor-icon.png)  
  
Conclua a caixa de diálogo **Conectar ao Servidor** se você não ainda estiver conectado a uma instância do SQL Server que você deseja monitorar.
  
## <a name="launch-activity-monitor-and-object-explorer-on-startup"></a>Inicie o Monitor de Atividade e Pesquisador de Objetos na inicialização
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  Na caixa de diálogo **Opções** , expanda **Ambiente**e selecione **Inicialização**.  
  
3.  Na lista suspensa **Na inicialização** , selecione **Abrir Pesquisador de Objetos e Monitor de Atividade**.  

4.  Clique em **OK**.
  
![open_object_explorer](../../relational-databases/performance-monitor/media/open-object-explorer.png)
  
  
## <a name="set-the-activity-monitor-refresh-interval"></a>Definir o intervalo de atualização do Monitor de Atividade  
  
1.   Abra o Monitor de Atividade.  
  
2.   Clique com o botão direito do mouse em **Visão Geral**, selecione **Intervalo de Atualização**e selecione o intervalo em que o Monitor de Atividade deve obter novas informações sobre a instância.  
  
  

