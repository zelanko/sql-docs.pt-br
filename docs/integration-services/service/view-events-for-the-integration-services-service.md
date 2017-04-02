---
title: "Exibir eventos para o servi&#231;o do Integration Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "eventos [Integration Services]"
  - "serviço [Integration Services], eventos"
  - "serviço Integration Services, eventos"
ms.assetid: 37e23946-10d1-4116-8568-8fd24067102e
caps.latest.revision: 21
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 21
---
# Exibir eventos para o servi&#231;o do Integration Services
  Há duas ferramentas nas quais você pode exibir eventos do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:  
  
-   A caixa de diálogo **Visualizador do Arquivo de Log** em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. A caixa de diálogo **Visualizador do Arquivo de Log** inclui opções para exportar, filtrar e pesquisar o log. Para obter mais informações sobre as opções do **Visualizador do Arquivo de Log**, consulte [Ajuda F1 do Visualizador do Arquivo de Log](../../relational-databases/logs/log-file-viewer-f1-help.md).  
  
-   O Visualizador de Eventos do Windows  
  
 Para obter descrições dos eventos registrados pelo serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], consulte [Eventos registrados pelo serviço Integration Services](../../integration-services/service/events-logged-by-the-integration-services-service.md).  
  
### Para exibir eventos do serviço para Integration Services no SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  No menu **Arquivo**, clique em **Conectar Pesquisador de Objetos**.  
  
3.  Na caixa de diálogo **Conectar ao Servidor**, selecione o tipo de servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], selecione ou localize o servidor com o qual se conectará e clique em **Conectar**.  
  
4.  No Pesquisador de Objetos, clique com o botão direito do mouse em [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e clique em **Exibir Logs**.  
  
5.  Para exibir eventos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], selecione **SQL Server Integration Services**. A opção **Eventos NT** é automaticamente marcada e desmarcada com a opção **SQL Server Integration Services**.  
  
### Para exibir eventos de serviço para Integration Services em Visualizador de Eventos do Windows  
  
1.  No **Painel de Controle**, se você estiver usando o Modo de exibição Clássico, clique em **Ferramentas Administrativas** ou, se estiver usando o Modo exibição de Categoria, clique em **Desempenho e Manutenção** e em **Ferramentas Administrativas**.  
  
2.  Clique em **Visualizador de Eventos**.  
  
3.  Na caixa de diálogo **Visualizador de Eventos**, clique em **Aplicativo**.  
  
4.  No snap-in **Aplicativo**, localize uma entrada na coluna **Fonte** que tem o valor **SQLISService**, clique com o botão direito do mouse na entrada e clique em **Propriedades**.  
  
5.  Opcionalmente, clique na seta para cima ou para baixo para exibir o próximo evento ou o anterior.  
  
6.  Opcionalmente, clique no ícone Copiar para Área de Transferência para copiar as informações do evento.  
  
7.  Escolha exibir dados de evento que usam bytes ou palavras.  
  
8.  Clique em **OK**.  
  
9. No menu **Arquivo**, clique em **Sair** para fechar a caixa de diálogo **Visualizador de Eventos**.  
  
## Consulte também  
 [Gerenciar o serviço Integration Services](../../integration-services/service/manage-the-integration-services-service.md)   
 [Adicionar um log para contadores de desempenho de fluxo de dados](../../integration-services/performance/add-a-log-for-data-flow-performance-counters.md)  
  
  