---
title: Erro de WMI 0x8007052f | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- 0x8007052f (WMI error)
ms.assetid: a33f12bd-15c4-42a8-b343-de44c3e87729
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 15e258cfe62b9b6cecdcaf3b1fc2f467ba92fab7
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="wmi-provider-error-0x8007052f"></a>Erro do Provedor WMI 0x8007052f
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do Evento|0x8007052f|  
|Origem do evento|Erro do Provedor WMI|  
|Componente|SQL Server Configuration Manager|  
|Nome simbólico|NA|  
|Texto da mensagem|Falha de logon: restrição na conta do usuário. As possíveis razões para isso são senhas em branco não permitidas, restrições de horário de logon ou uma restrição de política que foi aplicada.|  
  
## <a name="explanation"></a>Explicação  
 Este erro pode ocorrer quando você usa o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Gerenciador de Configurações para alternar para as contas internas (Serviço de Rede, Serviço Local ou Sistema Local) quando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está em execução em um Cluster do Windows Server ou em um Controlador de Domínio do Windows Server. Não execute serviços em contas internas de um Cluster do Windows Server ou de um Controlador de Domínio do Windows Server. Para recomendações sobre contas de serviço, consulte o tópico Configurando as contas de serviço do Windows nos Manuais Online do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="user-action"></a>Ação do usuário  
 Configure o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para usar uma conta de domínio.  
  
  
