---
title: Progresso do Supervisor de atualização | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], analysis progress status
- analyzing system [Upgrade Advisor], progress information
- SQL Server Upgrade Advisor, analysis progress status
- monitoring analysis progress
- progress information [Upgrade Advisor]
- status information [Upgrade Advisor]
ms.assetid: a9e3d1c8-d492-4beb-93c7-f1bc40d4a910
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f7efb9258203efcffeb98bf4404faee5f80aff9a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63016337"
---
# <a name="upgrade-advisor-progress"></a>Progresso do Supervisor de Atualização
  A análise do Supervisor de Atualização inicia com um analisador dedicado que faz uma análise de cada componente selecionado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Conforme os componentes são analisados, o progresso é indicado na **andamento** caixa de diálogo.  
  
## <a name="options"></a>Opções  
 **Ação**  
 Especifica o componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é selecionado para análise.  
  
 **Status**  
 Exibe o valor de status retornado pela interface de progresso do componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Mensagem**  
 Exibe mensagens de erro, falha ou de sucesso retornadas pelo analisador individual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Se a análise demorar muito tempo, você pode interrompê-la. Basta sair do Assistente para Análise do Supervisor de Atualização e depois executar novamente o assistente. Para reduzir o tempo da análise, selecione menos componentes para verificar.  
  
 Quando a análise estiver completa, o relatório será gravado em um arquivo. Você pode exibir o relatório clicando **Iniciar relatório** para iniciar o Visualizador de relatórios a partir desta página. Se você quiser exibir o relatório mais tarde, você pode abrir o **Visualizador de relatórios do Supervisor de atualização** da página inicial do Supervisor de atualização.  
  
> [!NOTE]  
>  Os relatórios anteriores são salvos sempre que você analisa um servidor. Os relatórios são salvos com o carimbo de data/hora do nome de arquivo. O visualizador de relatórios exibe os cinco relatórios mais recentes salvos.  
  
## <a name="see-also"></a>Consulte também  
 [Como: Iniciar o Supervisor de atualização](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [Como: Execute o Assistente para análise do Supervisor de atualização](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Componentes do SQL Server](../../../2014/sql-server/install/sql-server-components.md)   
 [Referência de Interface de usuário do Supervisor de atualização](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [Trabalhando com o Supervisor de Atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
