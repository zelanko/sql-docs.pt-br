---
title: Configurar o Reporting Services para usar um SAN (nome alternativo da entidade) | Microsoft Docs
description: Saiba como configurar o SQL Server Reporting Services e o Servidor de Relatórios do Power BI para usar um SAN modificando o arquivo rsreportserver.config e usando a ferramenta Netsh.exe.
ms.date: 09/27/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 40ddab224d24e566ad346d64d5238ca5c81d9f48
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891586"
---
# <a name="configure-reporting-services-to-use-a-subject-alternative-name-san"></a>Configurar o Reporting Services para usar um SAN (nome alternativo da entidade)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Este tópico explica como configurar o SSRS (Reporting Services) e o Servidor de Relatórios do Power BI para usar um SAN (nome alternativo da entidade) modificando o arquivo rsreportserver.config e usando a ferramenta Netsh.exe.

As instruções se aplicam à URL do serviço Web, bem como à URL do portal da Web na ferramenta Configuration Manager do Servidor de relatório.

Para usar um SAN, o certificado TLS/SSL deve estar registrado no servidor, estar assinado e ter a chave privada. Você não pode usar um certificado autoassinado.

As URLs no Reporting Services e no Servidor de Relatórios do Power BI podem ser configuradas para usar um certificado TLS/SSL. Um certificado normalmente tem apenas um nome de entidade, o que permite apenas uma URL por sessão de protocolo TSL, anteriormente conhecido como protocolo SSL. O SAN é um campo adicional no certificado que permite a um serviço TSL ouvir muitas URLs e compartilhar a porta TSL com outros aplicativos. Por exemplo, um SAN pode ser semelhante a `www.myreports.com`.

Para obter mais informações sobre configurações TSL para o Reporting Services, confira [Configurar conexões TLS em um servidor de relatório no modo nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md).  
  
## <a name="configure-to-use-a-subject-alternative-name-for-web-service-url"></a>Configurar para usar um nome alternativo da entidade para a URL do serviço Web
  
1.  Inicie o Configuration Manager do Servidor de Relatórios.  
  
     Para obter mais informações, confira [Gerenciador de Configurações do Servidor de Relatório&#40;modo nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
2.  Na página **URL do Serviço Web**, escolha uma porta TLS/SSL e o certificado TLS/SSL.  
  
     ![Gerenciador de configuração do servidor de relatório](../../reporting-services/report-server-sharepoint/media/reportingservices-configurationmanager.png "Gerenciador de configuração do servidor de relatório")  
  
     O Configuration Manager registra o certificado TLS/SSL para a porta.  
  
3.  Abra o arquivo rsreportserver.config.  
  
     Para o Modo nativo do SSRS 2016, o arquivo está localizado por padrão na seguinte pasta:  
  
    ```  
    \Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
     Para o SSRS 2017 e posteriores, o arquivo está localizado por padrão na seguinte pasta:  
  
    ```  
    \Program Files\Microsoft SQL Server Reporting Services\SSRS\ReportServer  
    ```  
    
     Para o Servidor de Relatórios do Power BI, o arquivo está localizado por padrão na seguinte pasta:  
  
    ```  
    \Program Files\Microsoft Power BI Report Server\PBIRS\ReportServer  
    ```  
  
4.  Copie a seção da URL para o aplicativo **ReportServerWebService**.
  
     Por exemplo, a seguinte seção de URL original é:  
  
    ```  
        <URL>  
         <UrlString>https://+:443</UrlString>  
         <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>  
         <AccountName>NT Service\ReportServer</AccountName>  
        </URL>  
  
    ```  
  
     A seguinte seção de URL modificada é:
  
    ```  
    <URL>  
         <UrlString>https://+:443</UrlString>  
         <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>  
         <AccountName>NT Service\ReportServer</AccountName>  
        </URL>  
        <URL>  
         <UrlString>https://www.myreports.com:443</UrlString>  
         <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051/AccountSid>  
         <AccountName>NT Service\ReportServer</AccountName>  
        </URL>  
  
    ```  
  
  > [!TIP]  
>  * Para o SSRS 2017 e posteriores, o valor de `AccountSid` é `S-1-5-80-4050220999-2730734961-1537482082-519850261-379003301` e o valor de `AccountName` é `NT SERVICE\SQLServerReportingServices`.
>  * Para o Servidor de Relatórios do Power BI, o valor de `AccountSid` é `S-1-5-80-1730998386-2757299892-37364343-1607169425-3512908663` e o valor de `AccountName` é `NT SERVICE\PowerBIReportServer`.
  
5.  Salve o arquivo rsreportserver.config.  
  
6.  Inicie um prompt de comando usando **Executar como Administrador** e execute a ferramenta Netsh.exe.  
  
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
    Reserved URL            : https://+:443/ReportServer/  
        User: NT SERVICE\ReportServer  
            Listen: Yes  
            Delegate: No  
            SDDL: D:(A;;GX;;;S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051)  
    ```  
  
     Uma urlacl é uma DACL (lista de controle de acesso discricionário) para uma URL reservada.  
  
9. Crie uma nova entrada para o nome alternativo da entidade, com o mesmo usuário e SDDL que a entrada existente, digitando o seguinte:  
  
    ```  
    netsh http>add urlacl  url=https://www.myreports.com:443/ReportServer    
    user="NT Service\ReportServer" sddl=D:(A;;GX;;;S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051)  
  
    ```  
  
10. Para a **URL do portal da Web**, crie uma entrada para o nome alternativo da entidade digitando o seguinte:

    ```  
    netsh http>add urlacl  url=https://www.myreports.com:443/Reports  
    user="NT Service\ReportServer" sddl=D:(A;;GX;;;S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051)  
  
    ```  
> [!TIP]  
>  * Para o SSRS 2017 e posteriores, o valor de `user` é `NT SERVICE\SQLServerReportingServices` e o valor de `sddl` é `D:(A;;GX;;;S-1-5-80-4050220999-2730734961-1537482082-519850261-379003301)`.
>  * Para o Servidor de Relatórios do Power BI, o valor de `user` é `NT SERVICE\PowerBIReportServer` e o valor de `sddl` é `S-1-5-80-1730998386-2757299892-37364343-1607169425-3512908663`

> [!NOTE]  
> Para o Servidor de Relatórios do Power BI, você precisa criar duas entradas adicionais para o nome alternativo da entidade digitando o seguinte:
>  * `add urlacl url=https://www.myreports.com:443/PowerBI user="NT SERVICE\PowerBIReportServer" sddl=D:(A;;GX;;;S-1-5-80-1730998386-2757299892-37364343-1607169425-3512908663)`
>  * `add urlacl url=https://www.myreports.com:443/wopi user="NT SERVICE\PowerBIReportServer" sddl=D:(A;;GX;;;S-1-5-80-1730998386-2757299892-37364343-1607169425-3512908663)`

11. Na página **Status do Servidor de Relatórios** do Configuration Manager do Servidor de Relatórios, clique em **Parar** e clique em **Iniciar** para reiniciar o servidor de relatórios.  
  
## <a name="see-also"></a>Confira também

 [Arquivo de configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Gerenciador de Configurações do Servidor de Relatório](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Modificar um arquivo de configuração do Reporting Services](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Configurar as URLs do Servidor de Relatório](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
