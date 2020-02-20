---
title: Limitar Histórico de Relatórios – Reporting Services | Microsoft Docs
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
ms.openlocfilehash: 2dd66078363e281c2a73bfcc70ba685493bc3b88
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67492599"
---
# <a name="limit-report-history---reporting-services"></a>Histórico de relatórios – Reporting Services
  O histórico de relatórios é uma coleção de instantâneos de relatórios que você cria. Você pode criar um histórico de relatórios sob demanda ou agendar com que frequência um instantâneo é criado e adicionado ao histórico de relatórios.  
  
 O histórico de relatórios é armazenado no banco de dados do servidor de relatórios. Se os instantâneos de relatório contiverem uma grande quantidade de dados, limite o histórico de relatórios para minimizar o efeito da retenção de instantâneos no tamanho do banco de dados.  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
## <a name="to-configure-report-history-for-a-report-server"></a>Para configurar o histórico de relatórios para um servidor de relatório  
  
1.  No Gerenciador de Relatórios, clique em **Configurações de Site** na barra de ferramentas global.  
  
2.  Selecione **Manter um número ilimitado de instantâneos no histórico de relatório** se desejar manter todo o histórico de relatórios indefinidamente. Caso contrário, selecione **Limitar as cópias do histórico de relatório** para especificar o número máximo de instantâneos que podem ser mantidos em um relatório específico.  
  
3.  Clique em **Aplicar**.  
  
## <a name="to-configure-report-history-for-a-specific-report"></a>Para configurar o histórico de relatórios para um relatório específico  
  
1.  No Gerenciador de Relatórios, navegue até o relatório para o qual deseja configurar o histórico e, em seguida, clique no relatório para abri-lo.  
  
2.  Clique no guia **Propriedades**.  
  
3.  Clique na guia **Histórico** .  
  
4.  Selecione as opções para seu relatório e clique em **Aplicar**. Para obter detalhes sobre cada opção, consulte [Página de propriedades Opções de Instantâneo &#40;Gerenciador de Relatórios&#41;](https://msdn.microsoft.com/library/f6641f59-5267-4f57-8957-63b93d1a9679).  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar um instantâneo ao histórico de relatório &#40;Gerenciador de Relatórios&#41;](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

## <a name="to-configure-report-history-for-a-report-server"></a>Para configurar o histórico de relatórios para um servidor de relatório  
  
1.  No portal da Web, clique em **Configurações do Site** na barra de ferramentas global.  
  
2.  Selecione **Manter um número ilimitado de instantâneos no histórico de relatório** se desejar manter todo o histórico de relatórios indefinidamente. Caso contrário, selecione **Limitar as cópias do histórico de relatório** para especificar o número máximo de instantâneos que podem ser mantidos em um relatório específico.  
  
3.  Clique em **Aplicar**.  
  
## <a name="to-configure-report-history-for-a-specific-report"></a>Para configurar o histórico de relatórios para um relatório específico  
  
1.  No portal da Web, navegue até o relatório para o qual deseja configurar o histórico e, em seguida, clique no relatório para abri-lo.  
  
2.  Clique no guia **Propriedades**.  
  
3.  Clique na guia **Histórico** .  
  
4.  Selecione as opções para seu relatório e clique em **Aplicar**. Para obter detalhes sobre cada opção, consulte [Página de propriedades Opções de Instantâneo](https://msdn.microsoft.com/library/f6641f59-5267-4f57-8957-63b93d1a9679).  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar um instantâneo ao histórico de relatório](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   

::: moniker-end
  
