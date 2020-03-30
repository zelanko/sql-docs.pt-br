---
title: Configurar a conta de serviço do servidor de relatório (Gerenciador de Configurações) | Microsoft Docs
description: O Reporting Services é implementado com um serviço que contém um serviço Web do servidor de relatório, um portal da Web e um aplicativo de processamento em segundo plano usado para o processamento agendado de relatórios e entrega de assinaturas.
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.custom: seo-lt-2019, seo-mmd-2019
ms.date: 12/04/2019
ms.openlocfilehash: 49a5f8e19db65691fe8e521d7ca6a65e828fe6bd
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74866019"
---
# <a name="configure-the-report-server-service-account-ssrs-configuration-manager"></a>Configurar a conta de serviço do servidor de relatório (Gerenciador de configurações SSRS)

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é implementado com um único serviço que contém um serviço Web do Servidor de Relatório, um [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]e um aplicativo de processamento em segundo plano usado para processamento agendado de relatórios e entrega de assinaturas. Este tópico explica como uma conta de serviço é configurada inicialmente e como modificar a conta ou a senha usando a ferramenta Configuração do Reporting Services.  
  
## <a name="initial-configuration"></a>Configuração inicial

 A conta de serviço do Servidor de Relatório é definida durante a Instalação. Você pode executar o serviço em uma conta de usuário do domínio ou uma conta interna, como uma **Conta de Serviço Virtual**. Não há nenhuma conta padrão. Qualquer conta especificada na página **Contas de Serviço** do Assistente de Instalação torna-se a conta inicial do serviço do Servidor de Relatório.  
  
> [!IMPORTANT]  
> Embora o serviço Web do Servidor de Relatório e o [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] sejam aplicativos do [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] separados, eles são executados em uma única arquitetura de serviço na mesma identidade de processo do Servidor de Relatório.

> [!NOTE]  
> Não há suporte para contas de serviço internas do Windows (Serviço Local ou Serviço de Rede) como contas de serviço do servidor de relatório em um computador que seja controlador de domínio.
  
## <a name="changing-the-service-account"></a>Alterando a conta de serviço

 Para exibir e reconfigurar as informações da conta de serviço, sempre use o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager. As informações sobre identidade de serviço são armazenadas internamente em vários locais. O uso da ferramenta garante que todas as referências sejam adequadamente atualizadas sempre que você alterar a conta ou a senha. O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager executa as seguintes etapas adicionais para garantir que o servidor de relatório permaneça disponível:  
  
- Adiciona automaticamente a nova conta para o grupo de servidor de relatório criado no computador local. Esse grupo é especificado nas ACLs (listas de controle de acesso) que protegem os arquivos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
- Atualiza automaticamente as permissões de logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] usada para hospedar o banco de dados do servidor de relatório. A nova conta é adicionada à **RSExecRole**.  
  
     O log do banco de dados da conta antiga não é removido automaticamente. Lembre-se de remover contas que não estejam mais sendo usadas. Para obter mais informações, confira [Administrar um banco de dados de servidor de relatório &#40;modo nativo do SSRS&#41;](../../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md).  
  
     A concessão de permissões do banco de dados para a nova conta de serviço ocorrerá apenas se você tiver configurado a conexão de banco de dados do servidor de relatório para usar a conta de serviço. Se tiver configurado a conexão do banco de dados do servidor de relatório para usar uma conta de usuário do domínio ou um logon do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , as informações sobre a conexão não terão sido afetadas pela atualização da conta de serviço.  
  
- Atualiza automaticamente a chave de criptografia para incluir as informações de perfil da conta nova.  
  
    > [!NOTE]  
    > Se o servidor de relatório fizer parte da implantação em expansão, somente o servidor de relatório que você está atualizando será afetado. As chaves de criptografia para outros servidores de relatório na implantação não são afetadas pela alteração da conta de serviço.  

## <a name="to-configure-the-report-server-service-account"></a>Para configurar a conta de serviço do Servidor de Relatório  
  
1. Inicie o gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e conecte-se ao servidor de relatório.  
  
2. Na página Conta de Serviço, selecione a opção que descreve o tipo de conta que você deseja usar.  
  
3. Se você tiver selecionado uma conta de usuário do Windows, especifique a nova conta e a senha. A conta não pode ter mais de 20 caracteres.  
  
     Se o servidor de relatório for implantado em uma rede compatível com a autenticação Kerberos, você precisará registrar o SPN (nome da entidade de serviço) do servidor de relatório com a conta de usuário de domínio que você tiver especificado. Para obter mais informações, consulte [Registrar um SPN &#40;Nome da Entidade de Serviço&#41; para um servidor de relatório](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md).  
  
4. Clique em **Aplicar**.  
  
5. Quando for solicitado que você faça backup da chave simétrica, digite um nome e um local de arquivo para o backup da chave simétrica, digite uma senha para bloquear e desbloquear o arquivo e clique em **OK**.  
  
6. Se o servidor de relatório usar a conta de serviço para conectar-se ao banco de dados do servidor de relatório, as informações de conexão serão atualizadas para usar a nova conta ou senha. A atualização das informações da conexão exige que você se conecte ao banco de dados. Se a caixa de diálogo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Conexão de Banco de Dados**do** for exibida, insira as credenciais que têm permissão para se conectar ao banco de dados e, em seguida, clique em **OK**.  
  
7. Quando for avisado para restaurar a chave simétrica, digite a senha que você especificou na etapa 5 e clique em **OK**.  
  
8. Revise as mensagens de status no painel Resultados para verificar se todas as tarefas foram concluídas com êxito.  
  
## <a name="choosing-an-account"></a>Escolhendo uma conta

 Para obter melhores resultados, especifique uma conta que tenha permissões de conexão de rede, com acesso aos controladores de domínio da rede e com gateways ou servidores SMTP corporativos. A tabela a seguir resume as contas e fornece recomendações para usá-las.  
  
|Conta|Explicação|  
|-------------|-----------------|  
|Contas de usuário de domínio|Se você tiver uma conta de usuário de domínio do Windows que possua as permissões mínimas necessárias para operações do servidor de relatório, deverá usá-la.<br /><br /> É recomendável uma conta de usuário de domínio porque ela isola o serviço Servidor de Relatório dos outros aplicativos. A execução de vários aplicativos em uma conta compartilhada, como Serviço de Rede, aumenta o risco de um usuário mal-intencionado assumir o controle do servidor de relatório, pois a violação de segurança de um aplicativo pode se estender facilmente a todos os aplicativos executados na mesma conta.<br /><br /> Se você usar uma conta de usuário de domínio, será necessário alterar a senha periodicamente, caso a organização imponha uma política de expiração de senha. Talvez também seja necessário registrar o serviço com a conta de usuário. Para obter mais informações, consulte [Registrar um SPN &#40;Nome da Entidade de Serviço&#41; para um servidor de relatório](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md).<br /><br /> Evite usar uma conta de usuário local do Windows. Normalmente, as contas locais não têm permissão suficiente para acessar recursos em outros computadores. Para obter mais informações sobre como o uso de uma conta local limita as funcionalidades do servidor de relatório, veja [Considerações sobre o uso de contas locais](#localaccounts) neste tópico.|  
|**Conta de Serviço Virtual**|**Conta de Serviço Virtual** representa o serviço Windows. É uma conta interna com menos privilégios que tem permissões de logon na rede. Essa conta é recomendada caso você não tenha uma conta de usuário de domínio disponível ou se quiser evitar interrupções de serviço que possam ocorrer em consequência de políticas de expiração de senha.|  
|**Serviço de Rede**|**Serviço de rede** é uma conta interna com menos privilégios que tem a permissões de logon na rede. <br /><br /> Se você selecionar **Serviço de Rede**, tente minimizar o número de serviços que são executados na mesma conta. Uma violação de segurança em qualquer aplicativo compromete a segurança de todos os outros aplicativos executados na mesma conta.|  
|**Serviço Local**|**Serviço Local** é uma conta interna semelhante a uma conta de usuário autenticada local do Windows. Os serviços executados como a conta **Serviço Local** acessam os recursos de rede como uma sessão nula sem credenciais. Essa conta não é apropriada para cenários de implantação de intranet em que o servidor de relatório deve se conectar a um banco de dados do servidor de relatório remoto ou a um controlador de domínio de rede para autenticar um usuário antes de abrir um relatório ou processar uma assinatura.|  
|**Sistema Local**|**Sistema Local** é uma conta altamente privilegiada que não é exigida para executar um servidor de relatório. Evite usar essa conta para instalações do servidor de relatório. Escolha uma conta de domínio ou um **Serviço de Rede** .|  
  
## <a name="considerations-for-using-local-accounts"></a><a name="localaccounts"></a> Considerações sobre o uso de contas locais

 A primeira questão a ser considerada ao usar contas locais é se o servidor de relatório exige acesso aos servidores de banco de dados remotos, aos servidores de email e aos controladores de domínio. Se você configurar o servidor de relatório para ser executado como uma conta de usuário local do Windows, um Serviço Local ou um Sistema Local, surgirão questões que deverão ser consideradas com relação à especificação das demais configurações e à criação e à entrega de assinaturas.  
  
- A execução do serviço em uma conta local limitará suas opções posteriormente se você configurar uma conexão com um banco de dados do servidor de relatório remoto. Especificamente, se você estiver usando um banco de dados do servidor de relatório remoto, será necessário configurar a conexão para que ela use uma conta de usuário de domínio ou um usuário do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tenha permissão para entrar na instância remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
- A execução do serviço em uma conta local criará requisitos para a criação de assinaturas. O servidor de relatório armazena informações sobre o usuário que cria a assinatura. Se o usuário criar uma assinatura enquanto estiver conectado em uma conta de domínio, o serviço do Servidor de Relatório tentará se conectar a um controlador de domínio para autenticar o usuário durante o processamento da assinatura. Se o serviço for executado em uma conta local, a solicitação de autenticação falhará assim que o servidor de relatório tentar enviar a solicitação a um controlador de domínio remoto. Para solucionar temporariamente essa limitação, o usuário pode usar uma extensão personalizada de autenticação com base em formulário ou conectar todos os usuários a um servidor de relatório em uma conta de usuário local.  
  
- A execução do serviço em uma conta local criará novos requisitos para a entrega de assinaturas. Algumas extensões de entrega têm informações da conta de usuário na definição da assinatura. Se você estiver enviando relatórios para endereços de email com base em contas de usuário de domínio e executar o serviço do Servidor de Relatório em uma conta local, o serviço não poderá acessar um controlador de domínio remoto para resolver a conta de email de destino.  
  
- Não há suporte para contas de serviço internas do Windows (Serviço Local ou Serviço de Rede) como contas de serviço do servidor de relatório em um computador que seja controlador de domínio.  
  
Os links e as diretrizes a seguir irão ajudá-lo a decidir qual a melhor opção para sua implantação.  
  
- [Configurar contas e permissões de serviço Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
- [The Services and Service Accounts Security Planning Guide](http://usergroup.doubletake.com/file_cabinet/download/0x000021733) (O guia de planejamento de segurança de serviços e de contas de serviço).  
  
## <a name="updating-an-expired-password"></a>Atualizando uma senha expirada

 Se o serviço do Servidor de Relatório for executado em uma conta de domínio e a senha expirar antes de ser atualizada no Gerenciador de Configurações do Reporting Services, o serviço não será iniciado até que seja especificada uma nova senha.  
  
 Se a senha da conta de serviço do [!INCLUDE[ssDE](../../includes/ssde-md.md)] expirar, ocorrerá o erro **rsReportServerDatabaseUnavailable** quando você tentar se conectar ao servidor de relatório. A redefinição da senha resolve esse erro.  
  
## <a name="troubleshooting-service-identity-update-errors"></a>Solucionando problemas de erros de atualização de identidade do serviço

 A alteração da identidade do serviço inicia uma série de eventos que incluem o reinício do serviço, a atualização da chave de criptografia protegida por senha, a atualização das reservas de URL e a atualização das informações de conexão de banco de dados do servidor de relatório, caso você esteja usando a conta de serviço para se conectar ao banco de dados do servidor de relatório. Você pode monitorar o status desses eventos pela exibição das notificações no painel Resultados, na parte inferior da página. Se ocorrerem erros durante esse processo, você poderá tentar resolvê-los usando as seguintes técnicas:  
  
- Se a chave simétrica não puder ser restaurada, você poderá tentar restaurá-la manualmente usando **Restaurar** na página Chaves de criptografia. Se isso não funcionar, considere a exclusão do conteúdo criptografado. Você precisará recriar as informações de conexão de fonte de dados e as assinaturas, mas o restante do conteúdo ainda estará disponível. Para saber mais, confira [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
- Se o serviço não for iniciado, reinicie-o manualmente usando o aplicativo de console Serviços nas Ferramentas do Administrador.  
  
- Podem ocorrer erros de reserva de URL ao atualizar a conta de serviço. Cada reserva de URL inclui um descritor de segurança que inclui uma DACL (Lista de Controle de Acesso Discricionário) que concede permissão à conta de serviço para aceitar solicitações na URL. Quando você atualizar a conta, a URL deverá ser recriada a fim de atualizar a DACL com as novas informações de conta. Se a reserva de URL não puder ser recriada e você souber que a conta é válida, tente reiniciar o computador. Se o erro persistir, tente usar uma conta diferente.  
  
## <a name="next-steps"></a>Próximas etapas

 [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)
