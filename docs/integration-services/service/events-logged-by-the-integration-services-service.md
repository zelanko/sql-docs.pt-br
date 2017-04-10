---
title: "Eventos registrados em log pelo servi&#231;o Integration Services Service | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "serviço [Integration Services], eventos"
  - "eventos [Integration Services], serviço"
  - "serviço do Integration Services, eventos"
ms.assetid: d4122dcf-f16f-47a0-93a2-ffa3d0d4f9cf
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# Eventos registrados em log pelo servi&#231;o Integration Services Service
  O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] registra várias mensagens no log de eventos de Aplicativo do Windows. O serviço registra essas mensagens quando é iniciado e interrompido e quando ocorrem determinados problemas.  
  
 Este tópico contém informações sobre as mensagens de evento comuns registradas pelo serviço no log de eventos de Aplicativo. O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] registra em log todas as mensagens descritas neste tópico com uma Origem de Evento de SQLISService.  
  
 Para obter informações gerais sobre o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], consulte [Serviço do Integration Services &#40;Serviço SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md).  
  
## Mensagens sobre o status do serviço  
 Quando você seleciona o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para instalação, o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é instalado e iniciado e o Tipo de Inicialização é definido como Automático.  
  
|ID do evento|Nome simbólico|Texto|Observações|  
|--------------|-------------------|----------|-----------|  
|256|DTS_MSG_SERVER_STARTING|Iniciando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] Service.|O serviço está prestes a iniciar.|  
|257|DTS_MSG_SERVER_STARTED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] Service iniciado.|O serviço foi iniciado.|  
|260|DTS_MSG_SERVER_START_FAILED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] Falha ao iniciar.%nErro: %1|Não foi possível iniciar o serviço. Essa incapacidade de iniciar pode ser o resultado de uma instalação danificada ou de uma conta de serviço inadequada.|  
|258|DTS_MSG_SERVER_STOPPING|Interrompendo o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] Service.% n%nInterromper todos os pacotes em execução ao sair:%1|O serviço está sendo interrompido e, se você configurá-lo para fazer isso, todos os pacotes em execução serão interrompidos. Você pode definir um valor verdadeiro ou falso no arquivo de configuração que determina se o serviço deve interromper a execução de pacotes quando o próprio serviço é interrompido. A mensagem desse evento inclui o valor desta configuração.|  
|259|DTS_MSG_SERVER_STOPPED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] Serviço interrompido.%nVersão do servidor %1|O serviço parou.|  
  
## Mensagens sobre o arquivo de configuração  
 As configurações do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] são armazenadas em um arquivo XML que pode ser modificado. Para obter mais informações, consulte [Configurando o serviço Integration Services &#40; Serviço SSIS&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md).  
  
|ID do evento|Nome simbólico|Texto|Observações|  
|--------------|-------------------|----------|-----------|  
|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] Serviço: %na configuração de Registro que especifica o arquivo de configuração não existe. %nTentando carregar o arquivo de configuração padrão.|A entrada do Registro que contém o caminho do arquivo de configuração não existe ou está vazia.|  
|272|DTS_MSG_SERVER_MISSING_CONFIG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] O arquivo de configuração de serviço não existe.%nCarregando com as configurações padrão.|O arquivo de configuração não existe no local especificado.|  
|273|DTS_MSG_SERVER_BAD_CONFIG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] O arquivo de configuração de serviço está incorreto.%nErro ao ler o arquivo de configuração: %1%n%nCarregando o servidor com as configurações padrão.|Não foi possível ler o arquivo de configuração ou ele não é válido. Talvez esse erro seja o resultado de um erro de sintaxe XML no arquivo.|  
  
## Outras mensagens  
  
|ID do evento|Nome simbólico|Texto|Observações|  
|--------------|-------------------|----------|-----------|  
|336|DTS_MSG_SERVER_STOPPING_PACKAGE|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] Serviço: interrompendo a execução do pacote.%nIdentificação de instância do pacote: %1%nIdentificação do pacote: %2%nNome do pacote: %3%nDescrição do pacote: %4%nPacote|O serviço está tentando interromper um pacote em execução. Você pode monitorar e interromper pacotes em execução no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para obter informações sobre como gerenciar pacotes no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], consulte [Gerenciamento de pacotes &#40;Serviço SSIS&#41;](../../integration-services/service/package-management-ssis-service.md).|  
  
## Tarefas relacionadas  
 Para obter informações sobre como exibir entradas de log, consulte [Exibir entradas de log na janela Eventos de Log](../../integration-services/performance/view-log-entries-in-the-log-events-window.md)  
  
## Consulte também  
 [Eventos registrados em log por um pacote do Integration Services](../../integration-services/performance/events-logged-by-an-integration-services-package.md)  
  
  