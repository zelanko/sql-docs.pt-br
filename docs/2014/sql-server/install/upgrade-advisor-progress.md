---
title: Andamento do supervisor de atualização | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
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
ms.openlocfilehash: 692b06051872084ff5e1b16dfaf1f8198a649d62
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062342"
---
# <a name="upgrade-advisor-progress"></a>Progresso do Supervisor de Atualização
  A análise do Supervisor de Atualização inicia com um analisador dedicado que faz uma análise de cada componente selecionado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. À medida que os componentes são analisados, o progresso é relatado na caixa de diálogo de **progresso** .  
  
## <a name="options"></a>Opções  
 **Ação**  
 Especifica o componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é selecionado para análise.  
  
 **Status**  
 Exibe o valor de status retornado pela interface de progresso do componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Message**  
 Exibe mensagens de erro, falha ou de sucesso retornadas pelo analisador individual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Se a análise demorar muito tempo, você pode interrompê-la. Basta sair do Assistente para Análise do Supervisor de Atualização e depois executar novamente o assistente. Para reduzir o tempo da análise, selecione menos componentes para verificar.  
  
 Quando a análise estiver completa, o relatório será gravado em um arquivo. Você pode exibir o relatório clicando em **Iniciar relatório** para iniciar o Visualizador de relatórios nesta página. Se desejar exibir o relatório mais tarde, você poderá abrir o **Visualizador de relatórios do supervisor de atualização** na página inicial do supervisor de atualização.  
  
> [!NOTE]  
>  Os relatórios anteriores são salvos sempre que você analisa um servidor. Os relatórios são salvos com o carimbo de data/hora do nome de arquivo. O visualizador de relatórios exibe os cinco relatórios mais recentes salvos.  
  
## <a name="see-also"></a>Consulte Também  
 [Como iniciar o supervisor de atualização](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [Como executar o assistente de análise do supervisor de atualização](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Componentes do SQL Server](../../../2014/sql-server/install/sql-server-components.md)   
 [Referência da interface do usuário do supervisor de atualização](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [Trabalhando com o Supervisor de Atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
