---
title: Criar histórico de relatórios (Reporting Services no modo integrado do SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report history [Reporting Services], SharePoint
ms.assetid: e57ec746-05ae-4ff6-8e39-6cde87310daa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2f9018ebb8225ee1d8f313474e82ac521b2646e7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66103902"
---
# <a name="create-report-history-reporting-services-in-sharepoint-integrated-mode"></a>Criar histórico de relatório (Reporting Services no modo integrado do SharePoint)
  O histórico de relatórios é uma coleção de instantâneos de relatórios que você cria. Cada instantâneo é uma cópia do relatório como existia quando criado. Ele inclui o layout e os dados que eram atuais para o relatório quando o instantâneo foi criado. Informações de renderização não são armazenadas com o instantâneo. Ao abrir um instantâneo no histórico de relatórios, ele é aberto em um novo HTML na Web Part do Visualizador de Relatórios. Depois de processado, você pode exportá-lo para outros formatos de aplicativo.  
  
 Para criar um histórico de relatórios, é necessário que o relatório seja executado como autônomo (ou seja, o servidor de relatório deve ser capaz de executar o relatório sem interação do usuário). É necessário ter a permissão Editar Itens na biblioteca que contém o relatório. Para exibir ou excluir o histórico de relatórios, é necessário ter a permissão Exibir Versões ou a permissão Excluir Versões.  
  
### <a name="to-create-a-snapshot-or-report-history-on-demand"></a>Para criar um instantâneo ou um histórico de relatórios sob demanda  
  
1.  Aponte para o relatório.  
  
2.  Clique para exibir a seta para baixo e selecione **Exibir Histórico de Relatórios**.  
  
3.  Clique em **Novo Instantâneo**. Se o botão não estiver visível, pode ser porque você não tem permissão para criar instantâneos do histórico de relatórios.  
  
4.  Para exibir o instantâneo recém-criado, selecione-o na lista. Cada instantâneo é identificado por um carimbo de data/hora que mostra quando ele foi criado. Você não pode renomear o instantâneo, movê-lo para outro local ou modificá-lo.  
  
### <a name="to-schedule-report-history"></a>Para agendar o histórico de relatórios  
  
1.  Aponte para o relatório.  
  
2.  Clique na seta para baixo e selecione **Gerenciar Opções de Processamento**.  
  
3.  Em **Opções de Instantâneo de Histórico**, clique em **Criar instantâneos de histórico de relatórios em um agendamento**.  
  
4.  Se você tiver uma agenda compartilhada que contenha as informações de agendamento que deseja usar, clique em **Em uma agenda compartilhada** e selecione a agenda que deseja usar. Caso contrário, clique em **Em uma agenda personalizada**e em **Configurar** para especificar as opções para criar o histórico de relatórios de acordo com uma agenda recorrente.  
  
### <a name="to-create-report-history-when-data-is-refreshed-in-a-report"></a>Para criar histórico de relatório quando dados são atualizados em um relatório  
  
1.  Aponte para o relatório.  
  
2.  Clique na seta para baixo e selecione **Gerenciar Opções de Processamento**.  
  
3.  Em **Opções de Instantâneo de Histórico**, clique em **Armazenar todos os instantâneos de dados de relatório no histórico de relatórios**.  
  
## <a name="see-also"></a>Consulte Também  
 [Definir opções de processamento &#40;Reporting Services no modo integrado do SharePoint&#41;](../set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
  
