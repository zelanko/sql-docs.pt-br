---
title: "Escolher a conta de serviço do agente para ambientes multisservidor | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, service accounts
- multiserver environments [SQL Server], SQL Server Agent service account behavior
ms.assetid: a07e2f38-281c-495b-965b-13fad03ba548
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ab8dd9c2e0c72072199314322f83cc28a21d10d4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="choose-the-right-sql-server-agent-service-account-for-multiserver-environments"></a>Escolher a conta de serviço do SQL Server Agent certa para ambientes multisservidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] A conta do Windows escolhida para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent pode afetar o comportamento de um ambiente multisservidor, da seguinte maneira:  
  
-   Se você executar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent sob uma conta que não seja membro do grupo Administradores do Windows local, a inscrição de servidores de destino em servidores mestre poderá falhar. Se isso acontecer, a seguinte mensagem de erro será retornada:  
  
    "A operação de inscrição falhou".  
  
    Reinicie os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para resolver o problema.  
  
-   Quando o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent é executado com a conta Sistema Local, só haverá suporte a operações de servidor mestre e servidor de destino se ambos residirem no mesmo computador. Se você usar essa configuração, a seguinte mensagem será retornada quando você inscrever servidores de destino para um servidor mestre:  
  
    "Verifique se a conta de inicialização de agente de *<target_server_computer_name>* tem direitos para fazer logon como um servidor de destino".  
  
    Você pode ignorar essa mensagem informativa. A operação de inscrição deve ser concluída com êxito.  
  
Para obter mais informações sobre como escolher uma conta para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, veja [Selecionar uma conta para o serviço do SQL Server Agent](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md).  
  
