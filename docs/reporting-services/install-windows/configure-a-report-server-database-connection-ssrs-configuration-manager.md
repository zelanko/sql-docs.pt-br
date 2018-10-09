---
title: Configurar uma conexão de banco de dados do servidor de relatório (Gerenciador de Configurações do SSRS) | Microsoft Docs
author: markingmyname
ms.author: maghan
manager: kfile
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.date: 09/20/2017
ms.openlocfilehash: eed0c630bca54b28e78f2c59c5a14fca6e77da54
ms.sourcegitcommit: 2da0c34f981c83d7f1d37435c80aea9d489724d1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48782315"
---
# <a name="configure-a-report-server-database-connection--ssrs-configuration-manager"></a>Configurar uma conexão de banco de dados do servidor de relatório (Gerenciador de configurações do SSRS)

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Cada instância do servidor de relatório requer uma conexão com o banco de dados do servidor de relatório que armazena relatórios, modelos de relatório, fontes de dados compartilhadas, recursos e metadados gerenciados pelo servidor. A conexão inicial poderá ser criada durante uma instalação do servidor de relatório se você estiver instalando a configuração padrão. Na maioria dos casos, você usará a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurar a conexão depois que Instalação for concluída. É possível modificar a conexão a qualquer momento para alterar o tipo de conta ou redefinir as credenciais. Para obter instruções passo a passo sobre como criar o banco de dados e configurar a conexão, consulte [Criar um banco de dados do servidor de relatório no modo nativo &#40;SSRS Gerenciador de Configurações&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).

 Você deve configurar uma conexão do banco de dados do servidor de relatório nas seguintes circunstâncias:  
  
-   Configurar um servidor de relatório para primeiro uso.  
  
-   Configurar um servidor de relatório para usar um banco de dados do servidor de relatório diferente.  
  
-   Alterar a conta ou a senha do usuário usadas para a conexão do banco de dados. Você só precisa atualizar a conexão do banco de dados quando as informações da conta estiverem armazenadas no arquivo RSReportServer.config. Se estiver usando a conta de serviço para a conexão (que usa a segurança integrada do Windows como o tipo de credencial) a senha não será armazenada, eliminando a necessidade de atualizar as informações da conexão. Para obter mais informações sobre como alterar contas, veja [Configurar a conta de serviço do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
-   Configurar uma implantação em expansão do servidor de relatório. A configuração de uma implantação em expansão requer que você crie várias conexões com um banco de dados do servidor de relatório. Para obter mais informações sobre como executar esta operação de várias etapas, consulte [Configurar uma implantação escalável do servidor de relatório no modo nativo &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).  
  
## <a name="how-reporting-services-connects-to-the-database-engine"></a>Como o Reporting Services se conecta ao Mecanismo de Banco de Dados  
 O acesso do servidor de relatório a um banco de dados do servidor de relatório depende de credenciais e informações de conexão, além de chaves de criptografia que sejam válidas para a instância do servidor de relatório que usa esse banco de dados. É necessário ter chaves de criptografia válidas para armazenar e recuperar dados confidenciais. As chaves de criptografia são criadas automaticamente quando você configura o banco de dados pela primeira vez. Depois que as chaves forem criadas, você deverá atualizá-las se alterar a identidade do serviço Servidor de Relatório. Para obter mais informações sobre como trabalhar com chaves de criptografia, consulte [Configurar e gerenciar chaves de criptografia &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).  
  
 O banco de dados do servidor de relatório é um componente interno, acessado somente pelo servidor de relatório. As credenciais e as informações de conexão especificadas para o banco de dados do servidor de relatório são usadas exclusivamente pelo servidor de relatório. Os usuários que solicitam relatórios não precisam de permissões de bancos de dados ou de um logon de banco de dados para o banco de dados do servidor de relatório.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa **System.Data.SqlClient** para se conectar ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda o banco de dados do servidor de relatório. Caso esteja usando uma instância local do [!INCLUDE[ssDE](../../includes/ssde-md.md)], o servidor de relatório estabelecerá a conexão usando memória compartilhada. Se você estiver usando um servidor de banco de dados remoto para o banco de dados do servidor de relatório, talvez precise habilitar conexões remotas, dependendo da edição que estiver usando. Se estiver usando a Enterprise Edition, as conexões remotas serão habilitadas para TCP/IP por padrão.  
  
 Para verificar se a instância aceita conexões remotas, clique em **Iniciar**, clique em **Todos os Programas**, clique em [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], clique em **Ferramentas de Configuração**, clique em **SQL Server Configuration Manager**e verifique se o protocolo TCP/IP está habilitado para cada serviço.  
  
 Quando você habilitar conexões remotas, os protocolos de cliente e de servidor também serão habilitados. Para verificar se os protocolos estão habilitados, clique em **Iniciar**, clique em **Todos os Programas**, clique em [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], clique em **Ferramentas de Configuração**, clique em **SQL Server Configuration Manager**, clique em **Configuração de Rede do SQL Server**e clique em **Protocolos para MSSQLSERVER**. Para obter mais informações, veja [Habilitar ou desabilitar um protocolo de rede de servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="defining-a-report-server-database-connection"></a>Definindo uma conexão do banco de dados do servidor de relatório  
 Para configurar a conexão, você deve usar a ferramenta Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou o utilitário de linha de comando **rsconfig** . Um servidor de relatório exige as seguintes informações de conexão:  
  
-   Nome da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda o banco de dados do servidor de relatório.  
  
-   Nome do banco de dados do servidor de relatório. Ao criar uma conexão pela primeira vez, é possível criar um novo banco de dados do servidor de relatório ou selecionar um banco de dados existente. Para obter mais informações, veja [Criar um banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md).  
  
-   Tipo de credencial. Você pode usar as contas de serviço, uma conta de domínio do Windows ou um logon de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Nome de usuário e senha (necessários apenas se você estiver usando uma conta de domínio do Windows ou um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ).  
  
 As credenciais fornecidas devem ter acesso ao banco de dados do servidor de relatório. Se você usar a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , essa etapa será executada automaticamente. Para obter mais informações sobre as permissões necessárias para acessar o banco de dados, consulte a seção "Permissões de banco de dados" deste tópico.  
  
### <a name="storing-database-connection-information"></a>Armazenando informações de conexão do banco de dados  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] armazena e criptografa as informações de conexão nas seguintes configurações do RSreportserver.config. Você deve usar a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou o utilitário rsconfig para criar valores criptografados para essas configurações.  
  
 Nem todos os valores são definidos para todo tipo de conexão. Se você configurar a conexão usando os valores padrão (ou seja, usando as contas de serviço para estabelecer a conexão), \<**LogonUser**>, \<**LogonDomain**> e \<**LogonCred**> estarão vazios, da seguinte maneira:  
  
```  
<Dsn></Dsn>  
<ConnectionType></ConnectionType>  
<LogonUser></LogonUser>  
<LogonDomain></LogonDomain>  
<LogonCred></LogonCred>  
```  
  
 Se você configurar a conexão para usar uma conta do Windows ou um logon de banco de dados específico, deverá se lembrar de atualizar os valores armazenados, caso altere a conta ou o logon posteriormente.  
  
### <a name="choosing-a-credential-type"></a>Escolhendo um tipo de credencial  
 Há três tipos de credenciais que podem ser usados em uma conexão com um banco de dados do servidor de relatório:  
  
-   Segurança integrada do Windows usando a conta de serviço do Servidor de Relatório. Como o servidor de relatório é implementado como um único serviço, somente a conta em que o serviço é executado exige acesso ao banco de dados.  
  
-   Uma conta de usuário do Windows. Se o servidor de relatório e o banco de dados do servidor de relatório estiverem instalados no mesmo computador, você poderá usar uma conta local. Caso contrário, deverá usar uma conta de domínio.  
  
-   Um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Não é possível usar uma extensão de autenticação personalizada para se conectar a um banco de dados do servidor de relatório. As extensões de autenticação personalizadas são usadas apenas para autenticar uma entidade para um servidor de relatório. Elas não afetam as conexões com o banco de dados do servidor de relatório ou as fontes de dados externas que fornecem conteúdo aos relatórios.  
  
 Se a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] for configurada para Autenticação do Windows e estiver no mesmo domínio ou em um domínio confiável com o computador do servidor de relatório, você poderá configurar a conexão para usar a conta de serviço ou uma conta de usuário do domínio que você gerencie como uma propriedade de conexão através da ferramenta de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se o servidor de banco de dados estiver em um domínio diferente ou se você estiver usando a segurança de grupo de trabalho, será necessário configurar a conexão para usar um logon de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Nesse caso, certifique-se de criptografar a conexão.  
  
##### <a name="using-service-accounts-and-integrated-security"></a>Usando contas de serviço e segurança integrada  
 Você pode usar a segurança integrada do Windows para se conectar pela conta de serviço do Servidor de Relatório. A conta recebe direitos de logon no banco de dados do servidor de relatório. Esse será o tipo de credencial padrão escolhido pela Instalação se você instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] na configuração padrão.  
  
 A conta de serviço é uma conta confiável que fornece uma abordagem de baixa-manutenção ao gerenciamento de uma conexão do banco de dados do servidor de relatório. Como a conta de serviço usa a segurança integrada do Windows para estabelecer a conexão, as credenciais não precisam ser armazenadas. Entretanto, se você alterar a senha ou a identidade da conta de serviço posteriormente (por exemplo, alternando de uma conta interna para uma conta do domínio), certifique-se de usar a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para fazer a alteração. A ferramenta atualiza automaticamente as permissões de banco de dados para usar as informações de conta revisadas. Para obter mais informações, veja [Configurar a conta de serviço do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
 Se você configurar a conexão do banco de dados para usar a conta de serviço, a conta deverá ter permissões de rede se o banco de dados do servidor de relatório estiver em um computador remoto. Não use a conta de serviço se o banco de dados do servidor de relatório estiver em um domínio diferente, atrás de um firewall ou se você estiver usando a segurança de grupo de trabalho em vez da segurança de domínio. Em vez disso, use uma conta de usuário do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##### <a name="using-a-domain-user-account"></a>Usando uma conta de usuário do domínio  
 Você pode especificar uma conta de usuário do Windows para a conexão do servidor de relatório com o banco de dados do servidor de relatório. Se você usar uma conta local ou de domínio, deverá atualizar a conexão do banco de dados do servidor de relatório sempre que alterar a senha ou a conta. Sempre use a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para atualizar a conexão.  
  
##### <a name="using-a-sql-server-login"></a>Usando um logon do SQL Server  
 Você pode especificar um único logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para se conectar ao banco de dados do servidor de relatório. Se você usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o banco de dados do servidor de relatório estiver em um computador remoto, use IPSec para ajudar a proteger a transmissão de dados entre os servidores. Se você usar um logon do banco de dados, deverá atualizar a conexão do banco de dados do servidor de relatório sempre que alterar a senha ou a conta.  
  
### <a name="database-permissions"></a>Permissões de banco de dados  
 As seguintes funções são concedidas às contas usadas para conexão com o banco de dados do servidor de relatório:  
  
-   Funções**public** e **RSExecRole** para o banco de dados **ReportServer** .  
  
-   Função**RSExecRole** para os bancos de dados **mestre**, **msdb**e **ReportServerTempdb** .  
  
 Quando você usar a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para criar ou modificar a conexão, essas permissões são concedidas automaticamente. Se você usar o utilitário rsconfig e estiver especificando uma conta diferente para a conexão, deverá atualizar o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para essa nova conta. Você pode criar arquivos de script na ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que atualizarão o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o servidor de relatório.  
  
### <a name="verifying-the-database-name"></a>Verificando o nome do banco de dados  
 Use a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para determinar qual banco de dados do servidor de relatório é usado por uma instância específica do servidor de relatório. Para localizar o nome, conecte-se à instância do servidor de relatório e abra a página Configuração do Banco de Dados.  
  
## <a name="using-a-different-report-server-database-or-moving-a-report-server-database"></a>Usando um banco de dados do servidor de relatório diferente ou movendo um banco de dados do servidor de relatório  
 Você pode configurar uma instância do servidor de relatório para usar um banco de dados do servidor de relatório diferente alterando as informações de conexão. Um caso comum para a alternância de bancos de dados é quando você implanta um servidor de relatório de produção. Normalmente, os servidores de produção são distribuídos por meio da alternância de um banco de dados do servidor de relatório de teste para um banco de dados do servidor de relatório de produção. Você também pode mover um banco de dados do servidor de relatório para outro computador. Para obter mais informações, veja [Atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="configuring-multiple-reports-servers-to-use-the-same-report-server-database"></a>Configurando vários servidores de relatório para usar o mesmo banco de dados do servidor de relatório  
 Você pode configurar vários servidores de relatório para usar o mesmo banco de dados do servidor de relatório. Essa configuração de implantação é chamada de implantação em expansão. Essa configuração será um pré-requisito se você deseja executar vários servidores de relatório em um cluster de servidores. Entretanto, você também pode usar essa configuração para segmentar aplicativos de serviço ou para testar a instalação e as configurações de uma nova instância do servidor de relatório a fim de compará-la com a instalação de um servidor de relatório existente. Para obter mais informações, veja [Configurar uma implantação em expansão do servidor de relatório em modo nativo &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).  

## <a name="next-steps"></a>Próximas etapas

[Criar um banco de dados do servidor de relatório](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)   
[Gerenciar um servidor de relatório de modo nativo do Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
[Configurar a conta de serviço do Servidor de Relatório](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
