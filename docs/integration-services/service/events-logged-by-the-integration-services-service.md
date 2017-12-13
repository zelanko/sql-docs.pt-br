---
title: "Eventos registrados em log pelo serviço Integration Services | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: service
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- service [Integration Services], events
- events [Integration Services], service
- Integration Services service, events
ms.assetid: d4122dcf-f16f-47a0-93a2-ffa3d0d4f9cf
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dc85b9b432cfccacabb6cf877e7f26edd4b0b975
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="events-logged-by-the-integration-services-service"></a>Eventos registrados em log pelo serviço Integration Services Service
  O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] registra várias mensagens no log de eventos de Aplicativo do Windows. O serviço registra essas mensagens quando é iniciado e interrompido e quando ocorrem determinados problemas.  
  
 Este tópico contém informações sobre as mensagens de evento comuns registradas pelo serviço no log de eventos de Aplicativo. O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] registra em log todas as mensagens descritas neste tópico com uma Origem de Evento de SQLISService.  
  
 Para obter informações gerais sobre o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], consulte [Serviço do Integration Services &#40;Serviço SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md).  
  
## <a name="service-status-messages"></a>Mensagens de status do serviço
 Quando você seleciona o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para instalação, o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é instalado e iniciado e o Tipo de Inicialização é definido como Automático.  
  
|ID do evento|Nome simbólico|Texto|Observações|  
|--------------|-------------------|----------|-----------|  
|256|DTS_MSG_SERVER_STARTING|Iniciando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] Service.|O serviço está prestes a iniciar.|  
|257|DTS_MSG_SERVER_STARTED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] Service iniciado.|O serviço foi iniciado.|  
|260|DTS_MSG_SERVER_START_FAILED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] Falha ao iniciar.%nErro: %1|Não foi possível iniciar o serviço. Essa incapacidade de iniciar pode ser o resultado de uma instalação danificada ou de uma conta de serviço inadequada.|  
|258|DTS_MSG_SERVER_STOPPING|Interrompendo o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] Service.% n%nInterromper todos os pacotes em execução ao sair:%1|O serviço está sendo interrompido e, se você configurá-lo para fazer isso, todos os pacotes em execução serão interrompidos. Você pode definir um valor verdadeiro ou falso no arquivo de configuração que determina se o serviço deve interromper a execução de pacotes quando o próprio serviço é interrompido. A mensagem desse evento inclui o valor desta configuração.|  
|259|DTS_MSG_SERVER_STOPPED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] Serviço interrompido.%nVersão do servidor %1|O serviço parou.|  
  
## <a name="settings-file-messages"></a>Mensagens de arquivo de configurações  
 As configurações do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] são armazenadas em um arquivo XML que pode ser modificado. Para obter mais informações, veja [Serviço Integration Services &#40;Serviço SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md).  
  
|ID do evento|Nome simbólico|Texto|Observações|  
|--------------|-------------------|----------|-----------|  
|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] Serviço: %na configuração de Registro que especifica o arquivo de configuração não existe. %nTentando carregar o arquivo de configuração padrão.|A entrada do Registro que contém o caminho do arquivo de configuração não existe ou está vazia.|  
|272|DTS_MSG_SERVER_MISSING_CONFIG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] O arquivo de configuração de serviço não existe.%nCarregando com as configurações padrão.|O arquivo de configuração não existe no local especificado.|  
|273|DTS_MSG_SERVER_BAD_CONFIG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] O arquivo de configuração de serviço está incorreto.%nErro ao ler o arquivo de configuração: %1%n%nCarregando o servidor com as configurações padrão.|Não foi possível ler o arquivo de configuração ou ele não é válido. Talvez esse erro seja o resultado de um erro de sintaxe XML no arquivo.|  
  
## <a name="other-messages"></a>Outras mensagens  
  
|ID do evento|Nome simbólico|Texto|Observações|  
|--------------|-------------------|----------|-----------|  
|336|DTS_MSG_SERVER_STOPPING_PACKAGE|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] Serviço: interrompendo a execução do pacote.%nIdentificação de instância do pacote: %1%nIdentificação do pacote: %2%nNome do pacote: %3%nDescrição do pacote: %4%nPacote|O serviço está tentando interromper um pacote em execução. Você pode monitorar e interromper pacotes em execução no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para obter informações sobre como gerenciar pacotes no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], consulte [Gerenciamento de pacotes &#40;Serviço SSIS&#41;](../../integration-services/service/package-management-ssis-service.md).|  

## <a name="view-events"></a>Exibir eventos
  Há duas ferramentas nas quais você pode exibir eventos do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] :  
  
-   A caixa de diálogo **Visualizador do Arquivo de Log** em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. A caixa de diálogo **Visualizador do Arquivo de Log** inclui opções para exportar, filtrar e pesquisar o log. Para obter mais informações sobre as opções do **Visualizador do Arquivo de Log**, consulte [Ajuda F1 do Visualizador do Arquivo de Log](../../relational-databases/logs/log-file-viewer-f1-help.md).  
  
-   O Visualizador de Eventos do Windows  
  
 Para obter descrições dos eventos registrados pelo serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , consulte [Eventos registrados pelo serviço Integration Services](../../integration-services/service/events-logged-by-the-integration-services-service.md).  
  
### <a name="to-view-service-events-for-integration-services-in-sql-server-management-studio"></a>Para exibir eventos do serviço para Integration Services no SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  No menu **Arquivo** , clique em **Conectar Pesquisador de Objetos**.  
  
3.  Na caixa de diálogo **Conectar ao Servidor** , selecione o tipo de servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , selecione ou localize o servidor com o qual se conectará e clique em **Conectar**.  
  
4.  No Pesquisador de Objetos, clique com o botão direito do mouse em [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e clique em **Exibir Logs**.  
  
5.  Para exibir eventos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , selecione **SQL Server Integration Services**. A opção **Eventos NT** é automaticamente marcada e desmarcada com a opção **SQL Server Integration Services** .  
  
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
 
## <a name="related-tasks"></a>Tarefas relacionadas  
 Para obter informações sobre como exibir entradas de log, consulte [Eventos registrados em log por um pacote do Integration Services](../../integration-services/performance/events-logged-by-an-integration-services-package.md)  
