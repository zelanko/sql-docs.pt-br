---
title: Configurar o Reporting Services para usar um nome alternativo do assunto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ce458f9f-4b4f-4a58-aa75-9a90dda1e622
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: a1b5ead3e2ab16eea905af3312779631ae6344ea
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56026757"
---
# <a name="configure-reporting-services-to-use-a-subject-alternative-name"></a>Configurar o Reporting Services para usar um nome alternativo da entidade
  Este tópico explica como configurar o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS) para usar um SAN (Nome alternativo da entidade) modificando o arquivo rsreportserver.config e usando a ferramenta Netsh.exe.  
  
||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Modo nativo|  
  
 As instruções aplicam-se à URL do Reporting Service e à URL do Serviço Web.  
  
 Para usar um SAN, o certificado SSL deve estar registrado no servidor, assinado e ter a chave privada. Você não pode usar um certificado autoassinado  
  
 Você pode configurar as URLs do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para usarem um certificado SSL. Um certificado normalmente tem apenas um nome de entidade, o que permite apenas uma URL por sessão SSL (protocolo SSL). O SAN é um campo adicional no certificado que permite que um serviço SSL ouça e seja válido para muitas URLs e compartilhe a porta SSL com outros aplicativos. O SAN é semelhante ao seguinte: www.s2.com.  
  
 Para obter mais informações sobre configurações SSL para [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], consulte [Configurar conexões SSL em um servidor de relatório do modo nativo](security/configure-ssl-connections-on-a-native-mode-report-server.md).  
  
### <a name="configure-ssrs-to-use-a-subject-alternative-name-for-web-service-url"></a>Configurar o SSRS para usar um nome alternativo da entidade para a URL do Web Service  
  
1.  Iniciar o Gerenciador de Configuração do Reporting Services.  
  
     Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
2.  Na página **URL do Serviço Web** , escolha uma porta SSL e o certificado SSL.  
  
     ![Gerenciador de Configurações do Reporting Services](media/reportingservices-configurationmanager.png "Gerenciador de Configurações do Reporting Services")  
  
     O gerente de configuração registra o certificado SSL para a porta.  
  
3.  Abra o arquivo rsreportserver.config.  
  
     Para o SSRS no modo Nativo, o arquivo RSReportServer.config está localizado por padrão na pasta abaixo.  
  
    ```  
    \Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
4.  Copie a seção da URL para o aplicativo Report Server Web Service.  
  
     Por exemplo, esta é a seção de URL original.  
  
    ```  
        <URL>  
         <UrlString>https://localhost:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
     Esta é a seção de URL modificada.  
  
    ```  
    <URL>  
         <UrlString>https://www.s1.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
        <URL>  
         <UrlString>https://www.s2.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
5.  Salve o arquivo rsreportserver.config.  
  
6.  Inicie um prompt de comando como administrador e execute a ferramenta Netsh.exe.  
  
    ```  
    C:\windows\system32\netsh  
    ```  
  
7.  Mude para o contexto http, digitando o seguinte:  
  
    ```  
    Netsh>http  
    ```  
  
8.  Mostre as urlacls existentes digitando o seguinte:  
  
    ```  
    Netsh http>show urlacl  
    ```  
  
     Uma entrada como a seguinte é exibida:  
  
    ```  
    Reserved URL            : https:// www.s1.com:443/ReportServer/  
        User: NT SERVICE\ReportServer  
            Listen: Yes  
            Delegate: No  
            SDDL: D:(A;;GX;;;S-1-5-80-1234567890-123456789-123456789-123456789-1234567890)  
    ```  
  
     Uma urlacl é uma DACL (lista de controle de acesso discricionário) para uma URL reservada.  
  
9. Crie uma nova entrada para o nome alternativo da entidade, com o mesmo usuário e SDDL que a entrada existente, digitando o seguinte:  
  
    ```  
    netsh http>add urlacl  url=https://www.s2.com:443/ReportServer    
    user="NT Service\ReportServer" sddl=D:(A;;GX;;;S-1-5-80-1234567980-12346579-123456789-123456789-1234567890)  
  
    ```  
  
10. Na página **Status do Servidor de Relatório** do Gerenciador de Configuração do Reporting Services, clique em **Parar** e clique em **Iniciar** para reiniciar o servidor de relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Arquivo de configuração RSReportServer](report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
