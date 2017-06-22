---
title: "Autenticação com o servidor de relatório | Microsoft Docs"
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
helpviewer_keywords:
- connections [Reporting Services], configuring
- connections [Reporting Services], accounts
- Windows authentication [Reporting Services]
- authentication [Reporting Services]
- Forms authentication
ms.assetid: 753c2542-0e97-4d8f-a5dd-4b07a5cd10ab
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c38fc293a297544710b77b52d054fae58273340e
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---

# <a name="authentication-with-the-report-server"></a>Autenticação com o servidor de relatório

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS) oferece várias opções configuráveis para autenticar usuários e aplicativos cliente em relação ao servidor de relatório. Por padrão, o servidor de relatório usa a Autenticação Integrada do Windows e supõe relações de confiança onde os recursos do cliente e da rede estão no mesmo domínio ou em um domínio confiável. Dependendo de sua topologia de rede e das necessidades de sua organização, você pode personalizar o protocolo de autenticação usado para a Autenticação Integrada do Windows, usar a autenticação básica ou usar uma extensão de autenticação baseada em formulários personalizada fornecida por você. Cada um dos tipos de autenticação pode ser ativado ou desativado individualmente. Você poderá habilitar mais de um tipo de autenticação se desejar que o servidor de relatório aceite solicitações de vários tipos.
  
 Todos os usuários ou aplicativos que solicitam acesso a conteúdo ou operações do servidor de relatório devem ser autenticados antes de o acesso ser permitido.  
  
## <a name="authentication-types"></a>Tipos de autenticação  
 Todos os usuários ou aplicativos que solicitam acesso a conteúdo ou operações do servidor de relatório devem ser autenticados com o tipo de autenticação configurado no servidor de relatório para que o acesso seja permitido. A tabela a seguir descreve os tipos de autenticação suportados pelo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
|Nome do tipo de autenticação|Valor da Camada de Autenticação HTTP|Usado por padrão|Description|  
|-----------------------------|-------------------------------------|---------------------|-----------------|  
|RSWindowsNegotiate|Negotiate|Sim|Tenta usar Kerberos para a Autenticação Integrada do Windows primeiro, mas reverterá para NTLM se o Active Directory não puder conceder um tíquete para a solicitação do cliente ao servidor de relatório. Negotiate só reverterá para NTLM se a permissão não estiver disponível. Se a primeira tentativa resultar em um erro que não seja de permissão ausente, o servidor de relatório não fará uma segunda tentativa.|  
|RSWindowsNTLM|NTLM|Sim|Usa NLTM para Autenticação Integrada do Windows.<br /><br /> As credenciais não serão delegadas ou representadas em outras solicitações. As solicitações subsequentes seguirão uma nova sequência de desafio/resposta. Dependendo das configurações de segurança de rede, talvez o usuário precise informar credenciais ou a solicitação de autenticação poderá ser processada de maneira transparente.|  
|RSWindowsKerberos|Kerberos|Não|Usa Kerberos para Autenticação Integrada do Windows. Você deve configurar o Kerberos por meio da configuração dos SPNs (nomes das entidades de serviço) para suas contas de serviço, o que exige privilégios de administrador de domínio. Se você configurar a delegação de identidade com o Kerberos, o token do usuário que está solicitando um relatório também poderá ser usado em uma conexão adicional com as fontes de dados externas que fornecem dados para relatórios.<br /><br /> Antes de especificar RSWindowsKerberos, certifique-se de que o navegador usado dá suporte a esse tipo de autenticação. Se você estiver usando o Microsoft Edge, ou Internet Explorer, a autenticação Kerberos só terá suporte por meio de Negotiate. O Microsoft Edge, ou Internet Explorer, não formulará uma solicitação de autenticação que especifique o Kerberos diretamente.|  
|RSWindowsBasic|Basic|Não|A autenticação Básica é definida no protocolo HTTP e só pode ser usada para autenticar solicitações HTTP no servidor de relatório.<br /><br /> As credenciais são transmitidas na solicitação HTTP em codificação base64. Se você usar a autenticação básica, use SSL para criptografar informações da conta de usuário antes de enviá-las pela rede. O SSL é um canal criptografado usado para enviar uma solicitação de conexão do cliente ao servidor de relatório por meio de uma conexão HTTP TCP/IP. Para obter mais informações, consulte o tópico sobre [Como usar SSL para criptografar dados confidenciais](http://go.microsoft.com/fwlink/?LinkId=71123) no site do [!INCLUDE[msCoName](../../includes/msconame-md.md)] TechNet.|  
|Personalizar|(Anônima)|Não|A autenticação Anônima orienta o servidor de relatório a ignorar o cabeçalho de autenticação em uma solicitação HTTP. O servidor de relatório aceita todas as solicitações, mas chama uma autenticação do Forms [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] personalizada especificada por você para autenticar o usuário.<br /><br /> Especifique **Personalizado** somente se estiver implantando um módulo de autenticação personalizada que processe todas as solicitações de autenticação no servidor de relatório. Você não pode usar o tipo de autenticação Personalizada com a extensão de Autenticação padrão do Windows.|  
  
## <a name="unsupported-authentication-methods"></a>Métodos de autenticação sem-suporte  
 Os métodos e solicitações de autenticação descritos a seguir não têm suporte.  
  
|Método de autenticação|Explicação|  
|---------------------------|-----------------|  
|Anônima|O servidor de relatório não aceitará solicitações não autenticadas de um usuário anônimo, a menos naquelas implantações que incluem uma extensão de autenticação personalizada.<br /><br /> O Construtor de Relatórios aceitará solicitações não autenticadas se você habilitar o acesso a ele em um servidor de relatório configurado para autenticação Básica.<br /><br /> Em todos os outros casos, as solicitações anônimas são rejeitadas com um erro Status HTTP 401 – Acesso Negado antes de a solicitação chegar a [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]. Os clientes que recebem o erro 401 de acesso negado devem reformular a solicitação com um tipo de autenticação válido.|  
|Tecnologias de logon único (SSO)|Não há suporte nativo para tecnologias de logon único no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para usar uma tecnologia de logon único, você deve criar uma extensão de autenticação personalizada.<br /><br /> O ambiente de hospedagem do servidor de relatório não dá suporte a filtros ISAPI. Se a tecnologia SSO que você está usando é implementada como filtro ISAPI, considere usar o suporte interno do ISA Server para RSASecueID ou o protocolo RADIUS. Do contrário, você poderá criar um filtro ISAPI do ISA Server ou HTTPModule para RS, mas é recomendável usar o ISA Server diretamente.|  
|Passport|Não tem suporte no SQL Server Reporting Services.|  
|Digest|Não tem suporte no SQL Server Reporting Services.|  
  
## <a name="configuration-of-authentication-settings"></a>Configuração dos parâmetros de autenticação  
 Configurações de autenticação são definidas para segurança padrão quando a URL do servidor de relatório é reservada. Se essas configurações forem modificadas incorretamente, o servidor de relatório retornará erros HTTP 401 – Acesso Negado para solicitações HTTP que não podem ser autenticadas. Para escolher um tipo de autenticação, você deve saber de que forma a Autenticação do Windows é suportada na rede. Especifique pelo menos um tipo de autenticação. Podem ser especificados vários tipos de autenticação para RSWindows. Os tipos de autenticação do RSWindows (ou seja, **RSWindowsBasic**, **RSWindowsNTLM**, **RSWindowsKerberos**e **RSWindowsNegotiate**) se excluem mutuamente com Personalizado.  
  
> [!IMPORTANT]  
>  O Reporting Services não valida as configurações especificadas para determinar se elas estão corretas para o ambiente de computação. É possível que a segurança padrão não funcione para a sua instalação ou que você especificará parâmetros de configuração inválidos para sua infraestrutura de segurança. Por isso, é importante testar a implantação do servidor de relatório com cautela no ambiente de teste controlado antes de disponibilizá-la para sua organização de uma maneira mais ampla.  
  
 O serviço Web Servidor de Relatórios e o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] sempre usam o mesmo tipo de autenticação. Não é possível configurar tipos de autenticação diferentes para as áreas de recurso do serviço Servidor de Relatórios. Se você tiver uma implantação em expansão, duplique todas as alterações feitas em todos os nós da implantação. Não é possível configurar nós diferentes na mesma implantação em expansão para usar tipos de autenticação diferentes.  
  
 O processamento em segundo plano não aceita solicitações de usuários finais, mas autentica todas as solicitações para fins de execução autônoma. Ele sempre usa a Autenticação do Windows e autentica solicitações usando o serviço Servidor de Relatórios ou a conta de execução autônoma caso esteja configurada.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Configurar a Autenticação do Windows no servidor de relatório](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)  
  
-   [Configurar a autenticação Básica no servidor de relatório](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md)  
  
-   [Configurar autenticação personalizada ou de formulários no servidor de relatório](../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Descrições das tarefas|Links|  
|-----------------------|-----------|  
|Configurar o tipo de Autenticação Integrada do Windows.|[Configurar a Autenticação do Windows no servidor de relatório](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)|  
|Configurar o tipo de Autenticação Básica.|[Configurar a autenticação Básica no servidor de relatório](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md)|  
|Configurar a autenticação de formulários ou um tipo de Autenticação Personalizada.|[Configurar autenticação personalizada ou de formulários no servidor de relatório](../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)|  
|Habilite o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] para tratar o cenário de autenticação personalizada.|[Configurar o portal da Web para passar cookies de autenticação personalizados](http://msdn.microsoft.com/en-us/91aeb053-149e-4562-ae4c-a688d0e1b2ba)|  

## <a name="next-steps"></a>Próximas etapas

[Concedendo permissões em um servidor de relatório no modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
[Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[Criar e gerenciar atribuições de função](../../reporting-services/security/create-and-manage-role-assignments.md)   
[Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
[Implementando uma extensão de segurança](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)   
[Configurar conexões SSL em um servidor de relatório do modo nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)   
[Configurar o acesso ao Construtor de Relatórios](../../reporting-services/report-server/configure-report-builder-access.md)   
[Visão geral de extensões de segurança](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
[Autenticação no Reporting Services](../../reporting-services/extensions/security-extension/authentication-in-reporting-services.md)   
[Autorização no Reporting Services](../../reporting-services/extensions/security-extension/authorization-in-reporting-services.md)  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
