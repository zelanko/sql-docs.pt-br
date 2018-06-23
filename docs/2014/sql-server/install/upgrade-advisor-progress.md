---
title: Progresso do Supervisor de atualização | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Upgrade Advisor [SQL Server], analysis progress status
- analyzing system [Upgrade Advisor], progress information
- SQL Server Upgrade Advisor, analysis progress status
- monitoring analysis progress
- progress information [Upgrade Advisor]
- status information [Upgrade Advisor]
ms.assetid: a9e3d1c8-d492-4beb-93c7-f1bc40d4a910
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e1b867360b773253ae22d24a76ce00b35c589d96
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020399"
---
# <a name="upgrade-advisor-progress"></a>Progresso do Supervisor de Atualização
  A análise do Supervisor de Atualização inicia com um analisador dedicado que faz uma análise de cada componente selecionado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Conforme os componentes são analisados, o progresso é relatado no **andamento** caixa de diálogo.  
  
## <a name="options"></a>Opções  
 **Ação**  
 Especifica o componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é selecionado para análise.  
  
 **Status**  
 Exibe o valor de status retornado pela interface de progresso do componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Mensagem**  
 Exibe mensagens de erro, falha ou de sucesso retornadas pelo analisador individual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Se a análise demorar muito tempo, você pode interrompê-la. Basta sair do Assistente para Análise do Supervisor de Atualização e depois executar novamente o assistente. Para reduzir o tempo da análise, selecione menos componentes para verificar.  
  
 Quando a análise estiver completa, o relatório será gravado em um arquivo. Você pode exibir o relatório clicando **Iniciar relatório** para iniciar o Visualizador de relatórios nessa página. Se você deseja exibir o relatório mais tarde, você pode abrir o **Visualizador de relatórios do Supervisor de atualização** na página de início do Supervisor de atualização.  
  
> [!NOTE]  
>  Os relatórios anteriores são salvos sempre que você analisa um servidor. Os relatórios são salvos com o carimbo de data/hora do nome de arquivo. O visualizador de relatórios exibe os cinco relatórios mais recentes salvos.  
  
## <a name="see-also"></a>Consulte também  
 [Como: iniciar o Supervisor de atualização](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [Como: executar o Assistente para análise do Supervisor de atualização](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Componentes do SQL Server](../../../2014/sql-server/install/sql-server-components.md)   
 [Referência de Interface de usuário do Supervisor de atualização](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [Trabalhando com o Supervisor de atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  