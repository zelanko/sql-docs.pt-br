---
title: Erro de WMI 0x8007052f | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: relational-databases-misc
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- 0x8007052f (WMI error)
ms.assetid: a33f12bd-15c4-42a8-b343-de44c3e87729
caps.latest.revision: 10
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 06f5b8000dcd43b12ed5d25ddc733fb892d385f3
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33700559"
---
# <a name="wmi-provider-error-0x8007052f"></a>Erro do Provedor WMI 0x8007052f
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
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
  
  
