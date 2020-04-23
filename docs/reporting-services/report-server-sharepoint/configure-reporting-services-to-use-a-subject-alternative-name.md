---
title: Configurar o Reporting Services para usar um nome alternativo da entidade | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 41a39c92a8ec9e9d940c44660a02abe5e710fede
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487019"
---
# <a name="configure-reporting-services-to-use-a-subject-alternative-name"></a>Configurar o Reporting Services para usar um nome alternativo da entidade

Este tópico explica como configurar o SSRS (Reporting Services) para usar um SAN (nome alternativo da entidade) modificando o arquivo rsreportserver.config e usando a ferramenta Netsh.exe.

As instruções aplicam-se à URL do Reporting Service e à URL do Serviço Web.

Para usar um SAN, o certificado TLS/SSL deve estar registrado no servidor, estar assinado e ter a chave privada. Você não pode usar um certificado autoassinado  
  
 As URLs no Reporting Services podem ser configuradas para usar um certificado TLS/SSL. Um certificado normalmente tem apenas um nome de entidade, o que permite apenas uma URL por sessão de protocolo TSL, anteriormente conhecido como protocolo SSL. O SAN é um campo adicional no certificado que permite a um serviço TSL ouvir muitas URLs e compartilhar a porta TSL com outros aplicativos. O SAN é semelhante a `www.s2.com`.  
  
 Para obter mais informações sobre configurações TSL para o Reporting Services, confira [Configurar conexões TLS em um servidor de relatório no modo nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md).  
  
## <a name="configure-ssrs-to-use-a-subject-alternative-name-for-web-service-url"></a>Configurar o SSRS para usar um nome alternativo da entidade para a URL do serviço Web
  
1.  Iniciar o Gerenciador de Configuração do Reporting Services.  
  
     Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
2.  Na página **URL do Serviço Web**, escolha uma porta TLS/SSL e o certificado TLS/SSL.  
  
     ![Gerenciador de Configurações do Reporting Services](../../reporting-services/report-server-sharepoint/media/reportingservices-configurationmanager.png "Gerenciador de Configurações do Reporting Services")  
  
     O Configuration Manager registra o certificado TLS/SSL para a porta.  
  
3.  Abra o arquivo rsreportserver.config.  
  
     Para o modo Nativo do SSRS, o arquivo está localizado por padrão na seguinte pasta:  
  
    ```  
    \Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
4.  Copie a seção da URL para o aplicativo Report Server Web Service.  
  
     Por exemplo, a seguinte seção de URL original é:  
  
    ```  
        <URL>  
         <UrlString>https://localhost:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
     A seguinte seção de URL modificada é:
  
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
  
## <a name="see-also"></a>Confira também

 [Arquivo de configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Gerenciador de Configurações do Reporting Services](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Modificar um arquivo de configuração do Reporting Services](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Configurar as URLs do Servidor de Relatório](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
