---
title: Erro de WMI 0x8007052f | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- 0x8007052f (WMI error)
ms.assetid: a33f12bd-15c4-42a8-b343-de44c3e87729
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d9fd50d33dbcc60cddf03a04d439f3b8630152a5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "35999952"
---
# <a name="wmi-error-0x8007052f"></a>Erro de WMI 0x8007052f
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|0x8007052f|  
|Origem do evento|Erro do Provedor WMI|  
|Componente|SQL Server Configuration Manager|  
|Nome simbólico|NA|  
|Texto da mensagem|Falha de logon: restrição na conta do usuário. As possíveis razões para isso são senhas em branco não permitidas, restrições de horário de logon ou uma restrição de política que foi aplicada.|  
  
## <a name="explanation"></a>Explicação  
 Este erro pode ocorrer quando você usa o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Gerenciador de Configurações para alternar para as contas internas (Serviço de Rede, Serviço Local ou Sistema Local) quando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está em execução em um Cluster do Windows Server ou em um Controlador de Domínio do Windows Server. Não execute serviços em contas internas de um Cluster do Windows Server ou de um Controlador de Domínio do Windows Server. Para recomendações sobre contas de serviço, consulte o tópico Configurando as contas de serviço do Windows nos Manuais Online do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="user-action"></a>Ação do usuário  
 Configure o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para usar uma conta de domínio.  
  
  