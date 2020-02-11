---
title: Conta de serviço (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.serviceaccount.F1
ms.assetid: face8120-4d32-4c6c-a1e8-99f27d1ff15d
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: db98f9806f48699af996a33675138150803e8812
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952390"
---
# <a name="service-account-ssrs-native-mode"></a>Conta do Serviço (modo nativo do SSRS)
  Use a página Conta de Serviço para especificar a conta em que o serviço Servidor de Relatório será executado. Essa conta é configurada inicialmente durante a Instalação. Você pode modificá-la se quiser alterar a conta ou a senha. O serviço Web Servidor de Relatórios, o Gerenciador de Relatórios e o aplicativo de processamento em segundo plano são executados na identidade de serviço especificada nesta página.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo.  
  
 A conta especificada no serviço Servidor de Relatório exige permissão para acessar o registro, os arquivos de programa do servidor de relatório e o banco de dados do servidor de relatório. Todas as permissões são configuradas automaticamente para a conta quando você usa o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para definir a conta. Se você usar a conta de serviço para se conectar ao banco de dados do servidor de relatório, o Configuration Manager criará um logon de banco de dados para a conta e configurará as permissões de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados atribuindo a conta ao RSExecRole na instância que hospeda o banco de dados do servidor de relatório. O banco de dados do servidor de relatório é o único repositório de dados em que um servidor de relatório pode gravar. A conta de serviço não exige permissões para nenhum outro repositório de dados.  
  
 Para abrir essa página, inicie o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e selecione o link no painel de navegação. Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
> [!IMPORTANT]  
>  Sempre que você precisar atualizar a conta ou a senha, será altamente recomendável usar o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . O uso do Gerenciador de Configurações para atualizar a conta garante que outras configurações internas que dependem da identidade do serviço sejam atualizadas de forma automática e simultânea.  
  
## <a name="options"></a>Opções  
 **Usar uma conta interna**  
 Selecione **Serviço de Rede**, **Sistema Local**ou **Serviço Local** na lista. Somente a opção **Serviço de Rede** é recomendada; porém, você pode configurar a conta para usar qualquer conta disponível.  
  
 **Usar outra conta**  
 Selecione essa opção para especificar uma conta de usuário do Windows. Você pode inserir uma conta de usuário local do Windows ou uma conta de usuário de domínio. Especifique uma conta de domínio neste formato: * \<domínio>\\<usuário\>*. Especifique uma conta de usuário do Windows local neste formato: * \<nome do \\ computador>\><usuário*. Só é possível selecionar uma conta existente; você não pode criar novas contas na Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 O limite máximo de caracteres na conta é 20.  
  
 Se sua rede usar autenticação Kerberos e você configurar o servidor de relatório para ser executado em uma conta de usuário de domínio, será necessário registrar o serviço com a conta de usuário. Para obter mais informações, consulte [Registrar um SPN &#40;Nome da Entidade de Serviço&#41; para um servidor de relatório](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md).  
  
 Se você alternar o tipo da conta (por exemplo, substituindo uma conta do Windows por outra ou substituindo uma conta interna por uma conta de domínio do Windows), precisará criar uma cópia de backup da chave de criptografia. A cópia de backup será restaurada automaticamente quando você selecionar a nova conta.  
  
> [!NOTE]  
>  O Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] solicitará que você faça o backup e restaure a chave de criptografia sempre que modificar a conta de serviço. Essas etapas são necessárias para assegurar que os dados criptografados permaneçam disponíveis para o servidor de relatório. Para obter mais informações sobre essas ações, consulte [chaves de criptografia &#40;o modo nativo do SSRS&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md).  
  
 Além disso, se houver um servidor de relatório configurado para execução no modo Integrado do SharePoint e você alterar a conta de serviço usando o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , também será necessário abrir a Administração Central do SharePoint e usar a página [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **do** para reaplicar as configurações de servidor de relatório e de instância. Essa etapa concederá à nova conta de serviço acesso a bancos de dados do SharePoint, o que é necessário para integrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a um produto ou uma tecnologia do SharePoint. Para obter mais informações sobre como conceder acesso ao banco de dados na administração central do SharePoint, consulte [configuração e administração de um servidor de relatório &#40;Reporting Services modo do sharepoint&#41;](../../../2014/reporting-services/configure-administer-report-server-reporting-services-sharepoint-mode.md) e [Reporting Services instalação do modo do sharepoint &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
## <a name="choosing-an-account"></a>Escolhendo uma conta  
 Para obter melhores resultados, especifique uma conta que tenha permissões de conexão de rede, com acesso aos controladores de domínio da rede e com gateways ou servidores SMTP corporativos. A tabela a seguir resume as contas e fornece recomendações para usá-las.  
  
|Conta|Explicação|  
|-------------|-----------------|  
|Contas de usuário de domínio|Se você tiver uma conta de usuário de domínio do Windows que possua as permissões mínimas necessárias para operações do servidor de relatório, deverá usá-la.<br /><br /> É recomendável uma conta de usuário de domínio porque ela isola o serviço Servidor de Relatório dos outros aplicativos. A execução de vários aplicativos em uma conta compartilhada, como Serviço de Rede, aumenta o risco de um usuário mal-intencionado assumir o controle do servidor de relatório, pois a violação de segurança de um aplicativo pode se estender facilmente a todos os aplicativos executados na mesma conta.<br /><br /> Uma conta de usuário de domínio será necessária se você estiver configurando o servidor de relatório para delegação restrita, ou para o modo integrado do SharePoint com Produtos do SharePoint 2010, que requerem contas de usuário de domínio em vez de contas de computador internas.<br /><br /> Observe que, se você usar uma conta de usuário de domínio, precisará alterar a senha periodicamente caso a empresa tenha uma política de expiração de senha. Talvez também seja necessário registrar o serviço com a conta de usuário. Para obter mais informações, consulte [Registrar um SPN &#40;Nome da Entidade de Serviço&#41; para um servidor de relatório](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md).<br /><br /> Evite usar uma conta de usuário local do Windows. Normalmente, as contas locais não têm permissão suficiente para acessar recursos em outros computadores. Para obter mais informações sobre como o uso de uma conta local limita as funcionalidades do servidor de relatório, veja [Considerações sobre o uso de contas locais](#localaccounts) neste tópico.|  
|**Serviço de rede**|**Serviço de rede** é uma conta interna com privilégios mínimos que tem permissões de logon de rede. Essa conta é recomendada caso você não tenha uma conta de usuário de domínio disponível ou se quiser evitar quaisquer interrupções de serviço que podem ocorrer em consequência de uma política de vencimento da senha.<br /><br /> Se você selecionar **Serviço de Rede**, tente minimizar o número de serviços que são executados na mesma conta. Uma violação de segurança em qualquer aplicativo comprometerá a segurança de todos os outros aplicativos executados na mesma conta.|  
|**Serviço local**|**Serviço local** é uma conta interna que é como uma conta de usuário do Windows local autenticada. Os serviços executados como a conta **Serviço Local** acessam os recursos de rede como uma sessão nula sem credenciais. Essa conta não é apropriada para cenários de implantação de intranet em que o servidor de relatório deve se conectar a um banco de dados do servidor de relatório remoto ou a um controlador de domínio de rede para autenticar um usuário antes de abrir um relatório ou processar uma assinatura.|  
|**Sistema local**|O **sistema local** é uma conta altamente privilegiada que não é necessária para executar um servidor de relatório. Evite usar essa conta para instalações do servidor de relatório. Escolha uma conta de domínio ou um **Serviço de Rede** .|  
  
##  <a name="localaccounts"></a>Considerações sobre o uso de contas locais  
 A primeira questão a ser considerada ao usar contas locais é se o servidor de relatório exige acesso aos servidores de banco de dados remotos, aos servidores de email e aos controladores de domínio. Se você configurar o servidor de relatório para ser executado como uma conta de usuário local do Windows, um Serviço Local ou um Sistema Local, surgirão questões que deverão ser consideradas com relação à especificação das demais configurações e à criação e à entrega de assinaturas.  
  
-   A execução do serviço em uma conta local limitará suas opções posteriormente, caso configure uma conexão para um banco de dados do servidor de relatório remoto. Especificamente, se você estiver usando um banco de dados do servidor de relatório remoto, precisará configurar a conexão de forma que ela utilize uma conta de usuário de domínio ou um usuário do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tenha permissão para fazer logon em uma instância remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   A execução do serviço em uma conta local criará novos requisitos de criação de assinaturas. O servidor de relatório armazena informações sobre o usuário que cria a assinatura. Se o usuário criar uma assinatura enquanto estiver conectado em uma conta de domínio, o serviço Servidor de Relatório tentará se conectar a um controlador de domínio para autenticar o usuário durante o processamento da assinatura. Se o serviço for executado em uma conta local, a solicitação de autenticação falhará assim que o servidor de relatório tentar enviar a solicitação a um controlador de domínio remoto. Para solucionar temporariamente essa limitação, o usuário pode usar uma extensão personalizada de autenticação com base em formulário ou conectar todos os usuários a um servidor de relatório em uma conta de usuário local.  
  
-   A execução do serviço em uma conta local criará novos requisitos para a entrega de assinaturas. Algumas extensões de entrega têm informações da conta de usuário na definição da assinatura. Se estiver enviando relatórios para endereços de email com base em contas de usuário de domínio e executar o serviço Servidor de Relatório em uma conta local, o serviço não poderá acessar um controlador de domínio remoto para resolver a conta de email de destino.  
  
-   Não há suporte para contas de serviço internas do Windows (Serviço Local ou Serviço de Rede) como contas de serviço do servidor de relatório em um computador que seja controlador de domínio.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar a conta de serviço do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurar uma conta de serviço &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)   
 [Gerenciador de Configurações do Reporting Services F1 tópicos de ajuda &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)  
  
  
