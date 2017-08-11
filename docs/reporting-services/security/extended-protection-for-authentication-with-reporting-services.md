---
title: "Proteção estendida para autenticação com o Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eb5c6f4a-3ed5-430b-a712-d5ed4b6b9b2b
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 3d0ba0f40d1d93f03a08b762d379cbe1242f0cd1
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---

# <a name="extended-protection-for-authentication-with-reporting-services"></a>Proteção Estendida para Autenticação com o Reporting Services

  A Proteção Estendida é um conjunto de melhorias das versões recentes do sistema operacional Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)] . A Proteção Estendida aprimora a maneira como as credenciais e a autenticação podem ser protegidas através de aplicativos. O recurso em si não oferece proteção diretamente contra ataques específicos, tais como encaminhamento de credenciais, mas oferece uma infraestrutura para aplicativos tais como [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para fiscalizar a Proteção Estendida para Autenticação.  
  
 Os principais aprimoramentos de autenticação que fazem parte de proteção estendida são a associação de serviço e a associação de canal. A associação de canal usa um token de associação de canal (CBT) para verificar se o canal estabelecido entre dois terminais não foi comprometido. A associação de serviço usa Nomes de Serviço Principais (SPN) para verificar o destino pretendido dos tokens de autenticação. Para obter mais informações básicas sobre a proteção estendida, consulte [Autenticação Integrada do Windows com Proteção Estendida](http://go.microsoft.com/fwlink/?LinkId=179922).  
  
SQL Server Reporting Services (SSRS) oferece suporte e impõe proteção estendida que foi habilitado no sistema operacional e configurada no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Por padrão, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aceita solicitações que especificam a autenticação Negotiate ou NTLM e, portanto, podem aproveitar o suporte à Proteção Estendida no sistema operacional e os recursos da proteção estendida do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Por padrão, a Proteção Estendida não está habilitada no o Windows. Para obter informações sobre como habilitar a Proteção Estendida no Windows, consulte [Proteção Estendida para Autenticação](http://go.microsoft.com/fwlink/?LinkID=178431). O sistema operacional e a pilha de autenticação de cliente devem suportar a Proteção Estendida de forma que a autenticação seja bem-sucedida. Para sistemas operacionais mais antigos, pode ser necessário instalar mais de uma atualização para um computador completo compatível com a Proteção Estendida. Para obter informações sobre os desenvolvimentos mais recentes da Proteção Estendida, consulte as informações atualizadas do [com a Proteção Estendida](http://go.microsoft.com/fwlink/?LinkId=183362).  

## <a name="reporting-services-extended-protection-overview"></a>Visão Geral da Proteção Estendida do Reporting Services

SSRS suporta e impõe proteção estendida que foi habilitada no sistema operacional. Se o sistema operacional não suportar a proteção estendida ou se o recurso não foi ativado no sistema operacional, o recurso de Proteção Estendida do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não conseguirá ser autenticado. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] também exige um Certificado de SSL. Para obter mais informações, veja [Configurar conexões SSL em um Servidor de Relatório do Modo Nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)  
  
> [!IMPORTANT]  
>  Por padrão, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não vem com a Proteção Estendida habilitada. O recurso pode ser habilitado por meio da modificação do arquivo de configuração **rsreportserver.config** ou por meio das APIs WMI para atualização do arquivo de configuração. SSRS não fornece uma interface do usuário para modificar ou exibir configurações de proteção de estendida. Para obter mais informações, consulte a seção [de parâmetros de configuração](#ConfigurationSettings) neste tópico.  
  
 Problemas que normalmente ocorrem em virtude de alterações nas configurações de proteção estendida ou de parâmetros incorretamente configurados não são expostos com mensagens de erro óbvias nem com janelas de caixa de diálogo. Problemas relacionados à configuração e à compatibilidade de proteção estendida geram falhas de autenticação e erros nos logs de rastreamento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Algumas tecnologias de acesso a dados podem não dar suporte à proteção estendida. Uma tecnologia de acesso a dados é usada para conexão às fontes de dados do SQL Server e ao banco de dados do catálogo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se uma tecnologia de acesso a dados não der suporte à proteção estendida, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] será afetado das seguintes maneiras:  
>   
>  -   O SQL Server que executa o banco de dados de catálogo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não pode ter a proteção estendida ativada; caso contrário, o servidor de relatório não se conectará com sucesso ao banco de dados de catálogo e gerará erros de autenticação.  
> -   Os servidores SQL Server usados como fontes de dados de relatórios [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não podem ter a proteção estendida habilitada. Caso contrário, as tentativas do servidor de relatório de se conectar à fonte de dados de relatório falharão e gerarão erros de autenticação.  
>   
>  A documentação de uma tecnologia de acesso a dados deve ter informações sobre suporte para proteção estendida.  
  
### <a name="upgrade"></a>Atualizar  
  
-   Atualizando um [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] server para o SQL Server 2016 adiciona parâmetros de configuração com valores padrão para o **rsreportserver. config** arquivo. Se as configurações já estavam presentes, a instalação do SQL Server 2016 preservará no **rsreportserver. config** arquivo.  
  
-   Quando os parâmetros de configuração forem acrescentados ao arquivo de configuração **rsreportserver.config** , o comportamento padrão será que o recurso da proteção estendida do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] esteja desativado e você deverá habilitar o recurso da forma descrita neste tópico. Para obter mais informações, consulte a seção [de parâmetros de configuração](#ConfigurationSettings) neste tópico.  
  
-   O valor padrão da configuração **RSWindowsExtendedProtectionLevel** é **Off**.  
  
-   O valor padrão da configuração **RSWindowsExtendedProtectionScenario** é **Proxy**.  
  
-   não verifica se o suporte à Proteção Estendida do sistema operacional ou da instalação atual do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está habilitada.  
  
### <a name="what-reporting-services-extended-protection-does-not-cover"></a>O que a proteção estendida do Reporting Services não contempla  
 As seguintes áreas de recursos e cenários não têm suporte no recurso de proteção estendida do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   Autores de extensões de segurança personalizadas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] devem acrescentar o suporte à proteção estendida à sua extensão de segurança personalizada.  
  
-   Componentes de terceiros adicionados ou usados por uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] devem ser atualizados pelo fornecedor para dar suporte à proteção estendida. Para obter mais informações, entre em contato com o fornecedor externo.  
  
## <a name="deployment-scenarios-and-recommendations"></a>Cenários e recomendações de implantação  
 Os cenários a seguir ilustram implantações e topologias diferentes e a configuração recomendada para protegê-los com a Proteção Estendida do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
### <a name="direct"></a>Direto  
 Este cenário descreve a conexão direta a um servidor de relatórios, por exemplo, um ambiente de intranet.  
  
|Cenário|Diagrama do cenário|Como proteger|  
|--------------|----------------------|-------------------|  
|Comunicação direta por SSL.<br /><br /> O servidor de relatórios irá impor ao cliente à Associação de Canal do servidor de relatórios.|![RS_ExtendedProtection_DirectSSL](../../reporting-services/security/media/rs-extendedprotection-directssl.gif "RS_ExtendedProtection_DirectSSL")<br /><br /> 1) Aplicativo cliente<br /><br /> 2) Servidor de relatórios|Defina **RSWindowsExtendedProtectionLevel** como **Allow** ou **Require**.<br /><br /> Defina **RSWindowsExtendedProtectionScenario** como **Direct**.<br /><br /> <br /><br /> - A associação de serviço não é necessária porque o canal de SSL será usado para a Associação de Canal.|  
|Comunicação direta por HTTP. O servidor de relatórios irá impor ao Cliente à Associação de Serviço do servidor de relatórios.|![RS_ExtendedProtection_Direct](../../reporting-services/security/media/rs-extendedprotection-direct.gif "RS_ExtendedProtection_Direct")<br /><br /> 1) Aplicativo cliente<br /><br /> 2) Servidor de relatórios|Defina **RSWindowsExtendedProtectionLevel** como **Allow** ou **Require**.<br /><br /> Defina **RSWindowsExtendedProtectionScenario** como **Any**.<br /><br /> <br /><br /> - Não há qualquer Canal de SSL. Portanto, imposições de Associação de Canal não são possíveis.<br /><br /> - A associação de serviço pode ser validada, entretanto, ela sozinha não constitui uma defesa completa sem a associação de Canal e a Associação de Serviço e só protegerá contra ameaças básicas.|  
  
### <a name="proxy-and-network-load-balancing"></a>Proxy e Balanceamento de Carga da Rede  
 Aplicativos clientes se conectam a um dispositivo ou software que executa o SSL e transmite as credenciais ao servidor para autenticação, por exemplo, um extranet, Internet ou Intranet Segura. O cliente se conecta a um Proxy ou todos os clientes usam um proxy.  
  
 A situação é a mesma quando você usa um dispositivo de Balanceamento de Carga de Rede (NLB).  
  
|Cenário|Diagrama do cenário|Como proteger|  
|--------------|----------------------|-------------------|  
|Comunicação por HTTP. O servidor de relatórios irá impor ao Cliente à Associação de Serviço do servidor de relatórios.|![RS_ExtendedProtection_Indirect](../../reporting-services/security/media/rs-extendedprotection-indirect.gif "RS_ExtendedProtection_Indirect")<br /><br /> 1) Aplicativo cliente<br /><br /> 2) Servidor de relatórios<br /><br /> 3)  Proxy|Defina **RSWindowsExtendedProtectionLevel** como **Allow** ou **Require**.<br /><br /> Defina **RSWindowsExtendedProtectionScenario** como **Any**.<br /><br /> <br /><br /> - Não há qualquer Canal de SSL. Portanto, imposições de Associação de Canal não são possíveis.<br /><br /> - O servidor de relatórios deve ser configurado para saber o nome do servidor de proxy para verificar se a associação de serviço é imposta corretamente.|  
|Comunicação por HTTP.<br /><br /> O servidor de relatórios irá impor ao cliente à Associação de Canal do Proxy e à Associação de Serviço de servidor de relatórios.|![RS_ExtendedProtection_Indirect_SSL](../../reporting-services/security/media/rs-extendedprotection-indirect-ssl.gif "RS_ExtendedProtection_Indirect_SSL")<br /><br /> 1) Aplicativo cliente<br /><br /> 2) Servidor de relatórios<br /><br /> 3)  Proxy|Defina <br />                    **RSWindowsExtendedProtectionLevel** para **Allow** ou **Require**.<br /><br /> Defina **RSWindowsExtendedProtectionScenario** como **Proxy**.<br /><br /> <br /><br /> - O canal SSL para o proxy está disponível. Portanto, a associação de canal para o proxy pode ser imposta.<br /><br /> - A Associação de Serviço também pode ser imposta.<br /><br /> O nome de Proxy deve ser conhecido pelo servidor de relatório e o administrador do servidor de relatório deverá criar uma reserva de URL para ele, com um cabeçalho de host, ou configurar o nome de Proxy na entrada **BackConnectionHostNames**do Registro do Windows.|  
|Comunicação indireta de HTTPS com um proxy seguro. O servidor de relatórios irá impor ao cliente à Associação de Canal do Proxy e o à Associação de Serviço de servidor de relatórios.|![RS_ExtendedProtection_IndirectSSLandHTTPS](../../reporting-services/security/media/rs-extendedprotection-indirectsslandhttps.gif "RS_ExtendedProtection_IndirectSSLandHTTPS")<br /><br /> 1) Aplicativo cliente<br /><br /> 2) Servidor de relatórios<br /><br /> 3)  Proxy|Defina <br />                    **RSWindowsExtendedProtectionLevel** para **Allow** ou **Require**.<br /><br /> Defina **RSWindowsExtendedProtectionScenario** como **Proxy**.<br /><br /> <br /><br /> - O canal SSL para o proxy está disponível. Portanto, a associação de canal para o proxy pode ser imposta.<br /><br /> - A Associação de Serviço também pode ser imposta.<br /><br /> O nome de Proxy deve ser conhecido pelo servidor de relatório e o administrador do servidor de relatório deverá criar uma reserva de URL para ele, com um cabeçalho de host, ou configurar o nome de Proxy na entrada **BackConnectionHostNames**do Registro do Windows.|  
  
### <a name="gateway"></a>Gateway  
 Este cenário descreve aplicativos Clientes que se conectam a um dispositivo ou software que realiza SSL e autentica o usuário. Então, o dispositivo ou software personifica o contexto de usuário ou o contexto de um usuário diferente antes de fazer uma solicitação ao servidor de relatórios.  
  
|Cenário|Diagrama do cenário|Como proteger|  
|--------------|----------------------|-------------------|  
|Comunicação indireta por HTTP.<br /><br /> O Gateway irá impor ao Cliente à associação de canal do Gateway. Há um Gateway para a Associação de Serviço de servidor de relatórios.|![RS_ExtendedProtection_Indirect_SSL](../../reporting-services/security/media/rs-extendedprotection-indirect-ssl.gif "RS_ExtendedProtection_Indirect_SSL")<br /><br /> 1) Aplicativo cliente<br /><br /> 2) Servidor de relatórios<br /><br /> 3) Dispositivo de gateway|Defina **RSWindowsExtendedProtectionLevel** como **Allow** ou **Require**.<br /><br /> Defina **RSWindowsExtendedProtectionScenario** como **Any**.<br /><br /> <br /><br /> - A Associação de Canal do cliente ao servidor de relatórios não é possível porque o gateway personifica um contexto e, portanto, cria um novo token de NTLM.<br /><br /> - Não há nenhum SSL do Gateway para o servidor de relatório. Portanto, a associação de canal não pode ser imposta.<br /><br /> - A Associação de Serviço pode ser imposta.<br /><br /> - O dispositivo de Gateway deve ser configurado pelo seu administrador para impor a associação de canal.|  
|Comunicação indireta de HTTPS com um gateway seguro. O Gateway irá impor ao cliente à Associação de Canal do Gateway e o servidor de relatórios irá impor ao Gateway à Associação de Canal do servidor de relatórios.|![RS_ExtendedProtection_IndirectSSLandHTTPS](../../reporting-services/security/media/rs-extendedprotection-indirectsslandhttps.gif "RS_ExtendedProtection_IndirectSSLandHTTPS")<br /><br /> 1) Aplicativo cliente<br /><br /> 2) Servidor de relatórios<br /><br /> 3) Dispositivo de gateway|Defina **RSWindowsExtendedProtectionLevel** como **Allow** ou **Require**.<br /><br /> Defina **RSWindowsExtendedProtectionScenario** como **Direct**.<br /><br /> <br /><br /> - A Associação de Canal do cliente ao servidor de relatórios não é possível porque o gateway personifica um contexto e, portanto, cria um novo token de NTLM.<br /><br /> - O SSL do Gateway para o servidor de relatórios significa que a associação de canal pode ser imposta.<br /><br /> - A Associação de Serviço não é obrigatória.<br /><br /> - O dispositivo de Gateway deve ser configurado pelo seu administrador para impor a associação de canal.|  
  
### <a name="combination"></a>Combinação  
 Este cenário descreve ambientes de Extranet ou Internet onde o cliente se conecta a um Proxy. Isso é combinado com um ambiente de intranet onde um cliente se conecta a um servidor de relatórios.  
  
|Cenário|Diagrama do cenário|Como proteger|  
|--------------|----------------------|-------------------|  
|Acesso indireto e direto do cliente ao serviço do servidor de relatórios sem SSL em conexões do cliente para o proxy ou do cliente para o servidor de relatórios.|1) Aplicativo cliente<br /><br /> 2) Servidor de relatórios<br /><br /> 3)  Proxy<br /><br /> 4) Aplicativo cliente|Defina **RSWindowsExtendedProtectionLevel** como **Allow** ou **Require**.<br /><br /> Defina **RSWindowsExtendedProtectionScenario** como **Any**.<br /><br /> <br /><br /> - A Associação de Serviço do cliente para o servidor de relatórios pode ser imposta.<br /><br /> O nome de Proxy deve ser conhecido pelo servidor de relatório e o administrador do servidor de relatório deverá criar uma reserva de URL para ele, com um cabeçalho de host, ou configurar o nome de Proxy na entrada **BackConnectionHostNames**do Registro do Windows.|  
|Acesso indireto e direto do cliente com o servidor de relatórios onde o cliente estabelece uma conexão SSL com o proxy ou servidor de relatórios.|![RS_ExtendedProtection_CombinationSSL](../../reporting-services/security/media/rs-extendedprotection-combinationssl.gif "RS_ExtendedProtection_CombinationSSL")<br /><br /> 1) Aplicativo cliente<br /><br /> 2) Servidor de relatórios<br /><br /> 3)  Proxy<br /><br /> 4) Aplicativo cliente|Defina **RSWindowsExtendedProtectionLevel** como **Allow** ou **Require**.<br /><br /> Defina **RSWindowsExtendedProtectionScenario** como **Proxy**.<br /><br /> <br /><br /> -A Associação de Canal pode ser usada<br /><br /> O nome de Proxy deve ser conhecido pelo servidor de relatório e o administrador do servidor de relatório deverá criar uma reserva de URL para o proxy, com um cabeçalho de host ou configurar o nome de Proxy na entrada **BackConnectionHostNames**do Registro do Windows.|  
  
## <a name="configuring-reporting-rervices-extended-protection"></a>Configurando a proteção estendida do Reporting Services  
 O arquivo **rsreportserver.config** contém os valores de configuração que controlam o comportamento da proteção estendida do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para obter mais informações sobre como usar e editar o arquivo de configuração do **rsreportserver.config** , consulte [Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md). As configurações da proteção estendida também podem ser alteradas e inspecionadas com APIs do WMI. Para obter mais informações, veja [Método SetExtendedProtectionSettings &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md).  
  
 Quando validação dos parâmetros de configuração falhar, os tipos de autenticação **RSWindowsNTLM**, **RSWindowsKerberos** e **RSWindowsNegotiate** são desativados no servidor de relatórios.  
  
###  <a name="ConfigurationSettings"></a> Parâmetros de configuração para a proteção estendida dos serviços de relatórios  
 A tabela a seguir fornece informações sobre os parâmetros de configuração que aparecem no **rsreportserver.config** para proteção estendida.  
  
|Configuração|Description|  
|-------------|-----------------|  
|**RSWindowsExtendedProtectionLevel**|Especifica o grau de imposição da proteção estendida. Os valores válidos são:<br /><br /> **Off**: padrão. Especifica que não há nenhuma verificação de associação de canal nem de associação de serviço.<br /><br /> **Allow** dá suporte à proteção estendida mas não a exige.  Especifica:<br /><br /> - A proteção estendida será imposta para aplicativos clientes executados em sistemas operacionais que dão suporte à proteção estendida. A maneira como a proteção é imposta é determinada pela configuração **RsWindowsExtendedProtectionScenario**<br /><br /> - A autenticação será permitida para aplicativos executados em sistemas operacionais que não dão suporte à proteção estendida.<br /><br /> **Require** especifica:<br /><br /> - A proteção estendida será imposta para aplicativos clientes executados em sistemas operacionais que dão suporte à proteção estendida.<br /><br /> A autenticação **não** será permitida para aplicativos executados em sistemas operacionais que não dão suporte para proteção estendida.|  
|**RsWindowsExtendedProtectionScenario**|Especifica que formas de proteção estendida serão validadas: Associação de Canal, Associação de Serviço ou ambas. Os valores válidos são:<br /><br /> **Proxy**: padrão. Especifica:<br /><br /> - A autenticação Windows NTLM, Kerberos e Negotiate quando um token de associação de canal estiver presente.<br /><br /> -A Associação de Serviço é imposta.<br /><br /> **Any** especifica:<br /><br /> - A autenticação Windows NTLM, Kerberos e Negotiate e uma associação de canal não são obrigatórias.<br /><br /> -A Associação de Serviço é imposta.<br /><br /> **Direct** especifica:<br /><br /> - A autenticação Windows NTLM, Kerberos e Negotiate quando um CBT estiver presente, uma conexão SSL com o serviço atual estiver presente e quando o CBT da conexão SSL corresponder ao CBT do token NTLM, Kerberos ou Negotiate.<br /><br /> - A Associação de Serviço não é imposta.<br /><br /> <br /><br /> Observação: a configuração **RsWindowsExtendedProtectionScenario** será ignorada se **RsWindowsExtendedProtectionLevel** for definido como **OFF**.|  
  
 Entradas de exemplo no arquivo de configuração **rsreportserver.config** :  
  
```  
<Authentication>  
         <RSWindowsExtendedProtectionLevel>Allow</RSWindowsExtendedProtectionLevel>  
         <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionLevel>  
</Authentication>  
```  
  
## <a name="service-binding-and-included-spns"></a>Associação de Serviço e SPNs incluídos  
 A associação de serviço usa SPNs (nomes de entidades de serviço) para validar o destino pretendido dos tokens de autenticação. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa as informações de reserva da URL existente para compilar uma lista de SPNs que são considerados válidos. Usando as informações de reserva de URLs para validação de SPNs e reservas de URL permite que os administradores do sistema a gerenciem ambos a partir de um único local.  
  
 A lista de SPNs válidos é atualizada quando o servidor de relatórios é iniciado, quando são alterados os parâmetros de configuração da proteção estendida ou quando o domínio do aplicativo é reciclado.  
  
 A lista válida de SPNs é específica para cada aplicativo. Por exemplo, o Gerenciador de Relatórios e o Servidor de Relatórios terão, cada um, uma lista diferente de SPNs válidos calculada.  
  
 A lista de SPNs válido calculada para um aplicativo é determinada pelos seguintes fatores:  
  
-   Cada reserva de URL.  
  
-   Cada SPN recuperado do controlador de domínio para a conta de serviço dos serviços de relatórios.  
  
-   Se uma reserva de URL contiver caracteres curinga ('*' ou '+'), o Servidor de Relatórios incluirá cada entrada da lista de hosts.  
  
### <a name="hosts-collection-sources"></a>Fontes de coleta de hosts.  
 A tabela a seguir lista as possíveis fontes da lista de Hosts.  
  
|Tipo da fonte.|Description|  
|--------------------|-----------------|  
|ComputerNameDnsDomain|O nome do domínio DNS atribuído ao computador local. Se o computador local for um nó de um cluster, será usado o nome de domínio DNS do servidor virtual de cluster.|  
|ComputerNameDnsFullyQualified|O nome DNS totalmente qualificado que identifica exclusivamente o computador local. Esse nome é uma combinação do nome de host do DNS e o nome de domínio do DNS, usando o formato *HostName*.*DomainName*. Se o computador local for um nó de um cluster, será usado o nome do DNS totalmente qualificado do servidor virtual de cluster.|  
|ComputerNameDnsHostname|O nome do host de DNS do computador local. Se o computador local for um nó de um cluster, será usado o nome de host do DNS do servidor virtual de cluster.|  
|ComputerNameNetBIOS|O nome NetBIOS do computador local. Se o computador local for um nó de um cluster, será usado o nome do NetBIOS do servidor virtual de cluster.|  
|ComputerNamePhysicalDnsDomain|O nome do domínio DNS atribuído ao computador local. Se o computador local for um nó de um cluster, será usado o nome do computador local e não o nome do servidor virtual de cluster.|  
|ComputerNamePhysicalDnsFullyQualified|O nome DNS totalmente qualificado que identifica exclusivamente o computador. Se o computador local for um nó de um cluster, será usado o nome do DNS totalmente qualificado do computador local e não o nome do servidor virtual de cluster.<br /><br /> O nome totalmente qualificado do DNS é uma combinação do nome de host do DNS e o nome de domínio do DNS, usando a forma *HostName*.*DomainName*.|  
|ComputerNamePhysicalDnsHostname|O nome do host de DNS do computador local. Se o computador local for um nó de um cluster, será usado o nome de host do DNS e não o nome do servidor virtual de cluster.|  
|ComputerNamePhysicalNetBIOS|O nome NetBIOS do computador local. Se o computador local for um nó de um cluster, será usado o nome do computador local e não do servidor virtual de cluster.|  
  
 À medida que SPNs são adicionados, uma entrada é adicionada ao log de rastreamento, que se assemelha ao seguinte:  
  
 `rshost!rshost!10a8!01/07/2010-19:29:38:: i INFO: SPN Whitelist Added <ComputerNamePhysicalNetBIOS> - <theservername>.`  
  
 `rshost!rshost!10a8!01/07/2010-19:29:38:: i INFO: SPN Whitelist Added <ComputerNamePhysicalDnsHostname> - <theservername>.`  
  
 Para obter mais informações, consulte [Registrar um Nome da Entidade de Serviço &#40;SPN&#41; para um Servidor de Relatório](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md) e [Sobre reservas e registro de URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md).  
  
## <a name="next-steps"></a>Próximas etapas

[Conectar-se ao mecanismo de banco de dados usando proteção estendida](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)   
[Visão geral sobre a Proteção Estendida para Autenticação](http://go.microsoft.com/fwlink/?LinkID=177943)   
[Autenticação Integrada do Windows com Proteção Estendida](http://go.microsoft.com/fwlink/?LinkId=179922)   
[Microsoft Security Advisory: Proteção estendida para autenticação](http://go.microsoft.com/fwlink/?LinkId=179923)   
[Log de rastreamento do serviço Servidor de Relatório](../../reporting-services/report-server/report-server-service-trace-log.md)   
[Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[Método SetExtendedProtectionSettings &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
