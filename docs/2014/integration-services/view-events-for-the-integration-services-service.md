---
title: Exibir eventos para o serviço de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- events [Integration Services]
- service [Integration Services], events
- Integration Services service, events
ms.assetid: 37e23946-10d1-4116-8568-8fd24067102e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4be91309e4feb34bd8dfd85aee8e3e0cd1f82ffd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66054669"
---
# <a name="view-events-for-the-integration-services-service"></a>Exibir eventos para o serviço do Integration Services
  Há duas ferramentas nas quais você pode exibir eventos do serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] :  
  
-   A caixa de diálogo **Visualizador do Arquivo de Log** em [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. A caixa de diálogo **Visualizador do Arquivo de Log** inclui opções para exportar, filtrar e pesquisar o log. Para obter mais informações sobre as opções do **Visualizador do Arquivo de Log**, consulte [Ajuda F1 do Visualizador do Arquivo de Log](../relational-databases/logs/log-file-viewer-f1-help.md).  
  
-   O Visualizador de Eventos do Windows  
  
 Para obter descrições dos eventos registrados pelo serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , consulte [Eventos registrados pelo serviço Integration Services](service/events-logged-by-the-integration-services-service.md).  
  
### <a name="to-view-service-events-for-integration-services-in-sql-server-management-studio"></a>Para exibir eventos do serviço para Integration Services no SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  No menu **Arquivo** , clique em **Conectar Pesquisador de Objetos**.  
  
3.  Na caixa de diálogo **Conectar ao Servidor** , selecione o tipo de servidor [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , selecione ou localize o servidor com o qual se conectará e clique em **Conectar**.  
  
4.  No Pesquisador de Objetos, clique com o botão direito do mouse em [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e clique em **Exibir Logs**.  
  
5.  Para exibir eventos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , selecione **SQL Server Integration Services**. A opção **Eventos NT** é automaticamente marcada e desmarcada com a opção **SQL Server Integration Services** .  
  
### <a name="to-view-service-events-for-integration-services-in-windows-event-viewer"></a>Para exibir eventos de serviço para Integration Services em Visualizador de Eventos do Windows  
  
1.  No **Painel de Controle**, se você estiver usando o Modo de exibição Clássico, clique em **Ferramentas Administrativas**ou, se estiver usando o Modo exibição de Categoria, clique em **Desempenho e Manutenção** e em **Ferramentas Administrativas**.  
  
2.  Clique em **Visualizador de Eventos**.  
  
3.  Na caixa de diálogo **Visualizador de Eventos** , clique em **Aplicativo**.  
  
4.  No snap-in **Aplicativo** , localize uma entrada na coluna **Fonte** que tem o valor **SQLISService**, clique com o botão direito do mouse na entrada e clique em **Propriedades**.  
  
5.  Opcionalmente, clique na seta para cima ou para baixo para exibir o próximo evento ou o anterior.  
  
6.  Opcionalmente, clique no ícone Copiar para Área de Transferência para copiar as informações do evento.  
  
7.  Escolha exibir dados de evento que usam bytes ou palavras.  
  
8.  Clique em **OK**.  
  
9. No menu **Arquivo** , clique em **Sair** para fechar a caixa de diálogo **Visualizador de Eventos** .  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar o serviço de Integration Services](../../2014/integration-services/manage-the-integration-services-service.md)   
 [Adicionar um log para contadores de desempenho de fluxo de dados](performance/performance-counters.md)  
  
  
