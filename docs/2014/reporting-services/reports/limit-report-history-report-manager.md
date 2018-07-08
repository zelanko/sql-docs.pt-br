---
title: Limitar o histórico de relatórios (Gerenciador de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- viewing report history
- report history [Reporting Services], viewing history
- report history [Reporting Services], configuring history
- historical data [Reporting Services]
- displaying report history
ms.assetid: 8e255792-d9ef-496f-a26c-9e969c1209a0
caps.latest.revision: 35
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e3e0f1978079b63499c39120fb47173cb603e657
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153747"
---
# <a name="limit-report-history-report-manager"></a>Limitar o histórico de relatório (Gerenciador de Relatórios)
  O histórico de relatórios é uma coleção de instantâneos de relatórios que você cria. Você pode criar um histórico de relatórios sob demanda ou agendar com que frequência um instantâneo é criado e adicionado ao histórico de relatórios.  
  
 O histórico de relatórios é armazenado no banco de dados do servidor de relatórios. Se os instantâneos de relatório contiverem uma grande quantidade de dados, limite o histórico de relatórios para minimizar o efeito da retenção de instantâneos no tamanho do banco de dados.  
  
### <a name="to-configure-report-history-for-a-report-server"></a>Para configurar o histórico de relatórios para um servidor de relatório  
  
1.  No Gerenciador de Relatórios, clique em **Configurações de Site** na barra de ferramentas global.  
  
2.  Selecione **Manter um número ilimitado de instantâneos no histórico de relatório** se desejar manter todo o histórico de relatórios indefinidamente. Caso contrário, selecione **Limitar as cópias do histórico de relatório** para especificar o número máximo de instantâneos que podem ser mantidos em um relatório específico.  
  
3.  Clique em **Aplicar**.  
  
### <a name="to-configure-report-history-for-a-specific-report"></a>Para configurar o histórico de relatórios para um relatório específico  
  
1.  No Gerenciador de Relatórios, navegue até o relatório para o qual deseja configurar o histórico e, em seguida, clique no relatório para abri-lo.  
  
2.  Clique na guia **Propriedades** .  
  
3.  Clique na guia **Histórico** .  
  
4.  Selecione as opções para seu relatório e clique em **Aplicar**. Para obter detalhes sobre cada opção, consulte [Página de propriedades Opções de Instantâneo &#40;Gerenciador de Relatórios&#41;](../snapshot-options-properties-page-report-manager.md).  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar um instantâneo ao histórico de relatórios &#40;Gerenciador de relatórios&#41;](../report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md)  
  
  
