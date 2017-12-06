---
title: "Modificar um arquivo de configuração do Reporting Services (RSreportserver.config) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 958ef51f-2699-4cb2-a92e-3b4322e36a30
caps.latest.revision: "9"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: d1b8d12e3b01fc8717770ae5fdb117f114ae324d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="modify-a-reporting-services-configuration-file-rsreportserverconfig"></a>Modify a Reporting Services Configuration File (RSreportserver.config)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] armazena configurações de aplicativo em um conjunto de arquivos de configuração. A instalação cria os arquivos de configuração para cada instância instalada do servidor de relatório. Em cada arquivo, os valores são definidos durante a instalação ou quando você usa ferramentas e aplicativos para configurar um servidor para operação. Em alguns casos, é necessário modificar um arquivo diretamente para adicionar ou definir configurações avançadas. As configurações são especificadas como elementos ou atributos XML. Se você entender de XML e arquivos de configuração, use um editor de texto ou de código para modificar configurações definidas pelo usuário.  
  
 Algumas configurações podem ser definidas somente com uma ferramenta. As configurações que contêm valores criptografados devem ser modificadas com a ferramenta Configuração do Reporting Services, o programa de Instalação ou o utilitário de linha de comando **rsconfig** . Você deve ser um membro do grupo Administradores local para executar estas ferramentas.  
  
> [!IMPORTANT]  
>  Tenha cuidado ao modificar arquivos de configuração. Se você modificar uma configuração que é reservada para uso interno, poderá desabilitar sua instalação. Geralmente, a modificação de configurações não é recomendada, a menos que você esteja tentando resolver um problema específico. Para obter mais informações sobre quais configurações podem ser alteradas com segurança, consulte [Arquivo de configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) ou [Arquivo de configuração RSReportDesigner](../../reporting-services/report-server/rsreportdesigner-configuration-file.md). Para obter mais informações sobre arquivos de configuração, confira a documentação do produto [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] .  
  
 Neste tópico:  
  
-   [Lendo e usando valores de configuração](#bkmk_read_values)  
  
-   [Sobre valores padrão](#bkmk_default_values)  
  
-   [Excluindo configurações](#bkmk_delete_config_settings)  
  
-   [Para editar um arquivo de configuração do Reporting Services](#bkmk_edit_configuation_file)  
  
##  <a name="bkmk_read_values"></a> Lendo e usando valores de configuração  
 Um servidor de relatório lê os arquivos de configuração quando o serviço é iniciado e sempre que o arquivo de configuração é salvo. Os valores novos e revisados entram em vigor em um novo domínio de aplicativo depois que o domínio de aplicativo atual expira. Sempre que possível, as solicitações que ainda estão sendo processadas no domínio de aplicativo atual podem ser concluídas. No entanto, algumas configurações requerem uma operação de reciclagem imediata do domínio de aplicativo. Neste caso, todas as solicitações em andamento são reinicializadas em um novo domínio de aplicativo.  
  
 Se o servidor de relatório detectar um valor inválido, registrará um erro no log de aplicativo do Windows e não será inicializado ou usará um valor padrão, dependendo do erro:  
  
-   Se o erro for XML danificado, o servidor de relatório não será inicializado. Se o servidor de relatório estiver em execução quando o erro for introduzido, ele ignorará o arquivo de configuração inválido até ser reinicializado ou até o domínio de aplicativo ser reciclado. Quando o erro for detectado, o servidor de relatório não será mais inicializado.  
  
-   Se o erro for um valor de configuração inválido, o servidor utilizará os valores padrão internos e registrará um erro nos arquivos de log de rastreamento. Em alguns casos, quando nenhum valor padrão interno está disponível, o servidor retorna o erro rsServerConfigurationError se a configuração inválida for crítica para as operações de servidor. Os erros sobre configurações críticas ausentes ou inválidas são retornadas ao aplicativo cliente em uma página de erro HTML e registrados no log de eventos.  
  
 Todas as alterações do arquivo de configuração, inclusive alterações bem-sucedidas, são registradas no arquivo de log de rastreamento do servidor de relatório. Somente erros são registrados no log de eventos de aplicativo.  
  
##  <a name="bkmk_default_values"></a> Sobre valores padrão  
 A maioria das configurações tem valores padrão que são especificados internamente no servidor de relatório. O servidor de relatório usa esses valores se um valor definido pelo usuário for inválido ou não for especificado. Se for necessário usar um valor padrão devido a uma configuração inválida, um erro será gravado no arquivo de log de rastreamento.  
  
##  <a name="bkmk_delete_config_settings"></a> Excluindo configurações  
 Para configurações que têm valores padrão, a remoção da configuração do arquivo de configuração não tem nenhum efeito. A maioria das configurações é definida e configurada de fato internamente. Se você excluir um item do arquivo de configuração, a cópia interna ainda estará disponível e usará o valor padrão definido para ela.  
  
##  <a name="bkmk_edit_configuation_file"></a> Para editar um arquivo de configuração do Reporting Services  
  
1.  Localize o arquivo de configuração que deseja editar:  
  
    -   O**RSReportServer.config** está localizado na seguinte pasta:  
  
        ```  
        C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer  
        ```  
        
        ||  
        |-|  
        |**[!INCLUDE[applies](../../includes/applies-md.md)]** Visualização Técnica de janeiro de 2017 dos relatórios do Power BI no SQL Server Reporting Services|
        
        ```  
        C:\Program Files\Microsoft SQL Server Reporting Services\RSServer\ReportServer
        ```
  
    -   O**RSReportServerServices.exe.config** está localizado na seguinte pasta:  
    
        > [!NOTE] 
        > Isso não está disponível no Technical Preview de janeiro de 2017 dos relatórios do Power BI no SQL Server Reporting Services.
  
        ```  
        C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer\bin  
        ```  
  
    -   O**RSReportDesigner.config** está localizado na seguinte pasta:  
  
        ```  
        C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies  
        ```  
  
2.  Salve uma cópia do arquivo caso precise reverter as alterações.  
  
3.  Abra o arquivo original no Bloco de Notas ou em um editor de código. Não use o editor de texto, pois ele define o comprimento do arquivo antes de salvá-lo, provocando a gravação de um erro de caractere inválido no arquivo de log de rastreamento.  
  
4.  Digite o elemento ou valor que deseja adicionar ou usar. Os elementos fazem distinção entre maiúsculas e minúsculas. Se você estiver adicionando um elemento, use as letras minúsculas e minúsculas corretas. Instruções específicas para editar arquivos de configuração estarão disponíveis se você estiver personalizando extensões de renderização, de autenticação ou de processamento de dados:  
  
    -   [Autenticação com o servidor de relatório](../../reporting-services/security/authentication-with-the-report-server.md)  
  
    -   [Configurar o portal da Web para passar cookies de autenticação personalizados](../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)
  
    -   [Personalizar parâmetros de extensão de renderização em RSReportServer.config](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)  
  
5.  Salve o arquivo.  
  
6.  Verifique os arquivos de log de rastreamento para observar se ocorreu algum erro. Se houver condições de erro, uma configuração ou seu valor foi especificado incorretamente. Examine o [Arquivo de configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) para obter valores válidos para qualquer configuração que esteja causando um erro. Para obter mais informações sobre como exibir o log de rastreamento, consulte [Log de rastreamento de serviço de servidor de relatório](../../reporting-services/report-server/report-server-service-trace-log.md).  
  
## <a name="see-also"></a>Consulte também  
 [Arquivo de configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Arquivo de configuração ReportingServicesService](../../reporting-services/report-server/reportingservicesservice-configuration-file.md)   
 [Arquivo de configuração RSReportDesigner](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [Implantando uma extensão de processamento de dados](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Implantando uma extensão de entrega](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)   
 [Implantando uma extensão de renderização](../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)   
 [Arquivos de configuração do Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md)  
  
  
