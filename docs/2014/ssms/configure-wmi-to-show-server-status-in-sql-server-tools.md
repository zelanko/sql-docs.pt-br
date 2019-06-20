---
title: Configurar o WMI para mostrar o status do servidor nas ferramentas do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- WMI Provider for Server Events, setting permissions
- WMI permissions [SQL Server]
ms.assetid: 7e97197b-ed4d-40d1-9a52-9ab1d92401d7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c0b0b8236187698917dddd3ca98830add6c3fde9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63245664"
---
# <a name="configure-wmi-to-show-server-status-in-sql-server-tools"></a>Configurar o WMI para mostrar o status do servidor nas ferramentas do SQL Server
  Este tópico descreve como configurar o WMI para mostrar o status de servidor nas ferramentas do SQL Server no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Na conexão com servidores, os componentes Servidores Registrados e Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], assim como o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager, usam o Windows Management Instrumentation (WMI) para obter o status dos serviços do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (MSSQLSERVER) e do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent (MSSQLSERVER). Para exibir o status do serviço, o usuário deve ter direitos para acessar o objeto WMI remotamente. O servidor deve ter o WMI instalado para que essa permissão possa ser configurada.  
  
##  <a name="SSMSProcedure"></a> Para configurar a permissão de WMI  
  
1.  No menu **Iniciar** no servidor remoto, clique em **Executar**.  
  
2.  No **aberto** caixa, digite `wmimgmt.msc`e, em seguida, clique em **Okey**.  
  
3.  No programa **Windows Management Infrastructure** , clique com o botão direito do mouse em **Controle WMI (Local)** e clique em **Propriedades**.  
  
4.  Na caixa de diálogo **Propriedades do Controle WMI (Local)** , na guia **Segurança** , expanda **Raiz**e clique em **CIMV2**.  
  
5.  Clique em **Segurança** para abrir a caixa de diálogo **Segurança de ROOT\CIMV2** .  
  
6.  Adicione um grupo ou usuário à caixa **Nomes de grupo ou de usuário** e selecione-o.  
  
7.  No **permissões para**_\<grupo ou usuário >_ caixa, selecione o **permitir** coluna, para o **habilitação remota** permissão , para que os usuários que desejam remotamente detectar o status do serviço.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar, parar ou pausar o serviço do SQL Server Agent](agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  
