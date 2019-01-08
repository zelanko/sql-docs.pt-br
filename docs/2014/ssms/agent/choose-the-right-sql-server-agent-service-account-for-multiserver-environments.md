---
title: Escolha a conta de serviço certa do SQL Server Agent para ambientes multisservidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, service accounts
- multiserver environments [SQL Server], SQL Server Agent service account behavior
ms.assetid: a07e2f38-281c-495b-965b-13fad03ba548
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e3a981690efb0139d8878cab4e13794fdcf44ed7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52762949"
---
# <a name="choose-the-right-sql-server-agent-service-account-for-multiserver-environments"></a>Escolher a conta de serviço do SQL Server Agent certa para ambientes multisservidor
  A conta do Windows escolhida para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pode afetar o comportamento de um ambiente multisservidor, da seguinte maneira:  
  
-   Se você executar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sob uma conta que não seja membro do grupo Administradores do Windows local, a inscrição de servidores de destino em servidores mestre poderá falhar. Se isso acontecer, a seguinte mensagem de erro será retornada:  
  
     "A operação de inscrição falhou".  
  
     Reinicie os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para resolver o problema.  
  
-   Quando o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é executado com a conta Sistema Local, só haverá suporte a operações de servidor mestre e servidor de destino se ambos residirem no mesmo computador. Se você usar essa configuração, a seguinte mensagem será retornada quando você inscrever servidores de destino para um servidor mestre:  
  
     "Verifique se a conta de inicialização de agente de *<target_server_computer_name>* tem direitos para fazer logon como um servidor de destino".  
  
     Você pode ignorar essa mensagem informativa. A operação de inscrição deve ser concluída com êxito.  
  
 Para obter mais informações sobre como escolher uma conta para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, veja [Selecionar uma conta para o serviço do SQL Server Agent](select-an-account-for-the-sql-server-agent-service.md).  
  
  
