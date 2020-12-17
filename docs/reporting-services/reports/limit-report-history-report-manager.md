---
title: Limitar Histórico de Relatórios – Reporting Services | Microsoft Docs
description: Saiba como configurar o histórico de relatórios para um servidor de relatório. Saiba também como configurar o histórico de relatórios para um relatório específico.
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- viewing report history
- report history [Reporting Services], viewing history
- report history [Reporting Services], configuring history
- historical data [Reporting Services]
- displaying report history
ms.assetid: 8e255792-d9ef-496f-a26c-9e969c1209a0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d01a008e00d2effccb109555799bbe6d55baf1e3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466567"
---
# <a name="limit-report-history---reporting-services"></a>Histórico de relatórios – Reporting Services
  O histórico de relatórios é uma coleção de instantâneos de relatórios que você cria. Você pode criar um histórico de relatórios sob demanda ou agendar com que frequência um instantâneo é criado e adicionado ao histórico de relatórios.  
  
 O histórico de relatórios é armazenado no banco de dados do servidor de relatórios. Se os instantâneos de relatório contiverem uma grande quantidade de dados, limite o histórico de relatórios para minimizar o efeito da retenção de instantâneos no tamanho do banco de dados.  

::: moniker range="=sql-server-2016"
  
## <a name="to-configure-report-history-for-a-report-server"></a>Para configurar o histórico de relatórios para um servidor de relatório  
  
1.  No Gerenciador de Relatórios, clique em **Configurações de Site** na barra de ferramentas global.  
  
2.  Selecione **Manter um número ilimitado de instantâneos no histórico de relatório** se desejar manter todo o histórico de relatórios indefinidamente. Caso contrário, selecione **Limitar as cópias do histórico de relatório** para especificar o número máximo de instantâneos que podem ser mantidos em um relatório específico.  
  
3.  Clique em **Aplicar**.  
  
## <a name="to-configure-report-history-for-a-specific-report"></a>Para configurar o histórico de relatórios para um relatório específico  
  
1.  No Gerenciador de Relatórios, navegue até o relatório para o qual deseja configurar o histórico e, em seguida, clique no relatório para abri-lo.  
  
2.  Clique no guia **Propriedades**.  
  
3.  Clique na guia **Histórico** .  
  
4.  Selecione as opções para seu relatório e clique em **Aplicar**. Para obter detalhes sobre cada opção, consulte [Página de propriedades Opções de Instantâneo &#40;Gerenciador de Relatórios&#41;](/previous-versions/sql/sql-server-2016/ms189952(v=sql.130)).  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar um instantâneo ao histórico de relatório &#40;Gerenciador de Relatórios&#41;](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../web-portal-ssrs-native-mode.md)  

::: moniker-end

::: moniker range=">=sql-server-2017"

## <a name="to-configure-report-history-for-a-report-server"></a>Para configurar o histórico de relatórios para um servidor de relatório  
  
1.  No portal da Web, clique em **Configurações do Site** na barra de ferramentas global.  
  
2.  Selecione **Manter um número ilimitado de instantâneos no histórico de relatório** se desejar manter todo o histórico de relatórios indefinidamente. Caso contrário, selecione **Limitar as cópias do histórico de relatório** para especificar o número máximo de instantâneos que podem ser mantidos em um relatório específico.  
  
3.  Clique em **Aplicar**.  
  
## <a name="to-configure-report-history-for-a-specific-report"></a>Para configurar o histórico de relatórios para um relatório específico  
  
1.  No portal da Web, navegue até o relatório para o qual deseja configurar o histórico e, em seguida, clique no relatório para abri-lo.  
  
2.  Clique no guia **Propriedades**.  
  
3.  Clique na guia **Histórico** .  
  
4.  Selecione as opções para seu relatório e clique em **Aplicar**. Para obter detalhes sobre cada opção, consulte [Página de propriedades Opções de Instantâneo](/previous-versions/sql/sql-server-2016/ms189952(v=sql.130)).  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar um instantâneo ao histórico de relatório](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   

::: moniker-end
