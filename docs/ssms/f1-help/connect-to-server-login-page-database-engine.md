---
title: Conectar ao Mecanismo de Banco de Dados do Servidor (página Logon) | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c3d6f51174198474046eb8c5a6155270a1445ccc
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265089"
---
# <a name="connect-to-server-login-page-database-engine"></a>Conectar ao Servidor (página Logon) Mecanismo de Banco de Dados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Use essa guia para exibir ou especificar opções ao se conectar ao [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]. Na maioria das vezes, é possível conectar-se informando o nome do computador do servidor de banco de dados na caixa **Nome do servidor** e clicando em **Conectar**. Se você estiver se conectando a uma instância nomeada, use o nome do computador seguido por uma barra invertida e o nome da instância. Por exemplo, `mycomputer\myinstance`. Se você estiver se conectando ao [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)], use o nome do computador seguido por **\sqlexpress**.  
  
Muitos fatores podem afetar sua possibilidade de conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter ajuda, consulte os seguintes recursos:  
- [Tutorial – Lição 1: Conectando-se ao Mecanismo de Banco de Dados](../../relational-databases/lesson-1-connecting-to-the-database-engine.md)  
- [Solucionar problemas na conexão com o Mecanismo de Banco de Dados do SQL Server](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)  
- [Solving Connectivity errors to SQL Server](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server) (Resolvendo erros de conectividade com o SQL Server)    
  
> [!NOTE]  
> Para se conectar usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá ser configurado no modo de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows. Para obter mais informações sobre como determinar o modo de autenticação e para alterar esse modo, confira [Como: Alterar modo de autenticação do servidor](../../database-engine/configure-windows/change-server-authentication-mode.md).  
  
## <a name="options"></a>Opções  
**Tipo de servidor**  
Ao registrar um servidor a partir do Pesquisador de Objetos, selecione o tipo de servidor ao qual se conectar: [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services ou Integration Services. O restante da caixa de diálogo mostra somente as opções que se aplicam ao tipo de servidor selecionado. Ao registrar um servidor de Servidores Registrados, a caixa **Tipo de servidor** é somente leitura e corresponde ao tipo de servidor exibido no componente Servidores Registrados. Para registrar outro tipo de servidor, selecione [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services ou Integration Services na barra de ferramentas Servidores Registrados antes de iniciar o registro de um novo servidor.  
  
Ao conectar-se a uma instância do Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], você deve usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e especificar um banco de dados na caixa de diálogo **Conectar ao Servidor** , na guia **Propriedades da Conexão** . Verifique se você marcou a caixa de seleção **Criptografar conexão** .  
  
Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conecta-se ao **mestre**. Se você especificar um banco de dados do usuário, somente esse banco de dados e seus objetos serão exibidos no Pesquisador de Objetos. Se você se conectar ao **mestre**, todos os bancos de dados serão exibidos. Confira mais informações em [Visão geral do Banco de Dados SQL do Microsoft Azure](/azure/sql-database/sql-database-technical-overview/).
  
**Nome do servidor**  
Selecione a instância do servidor com a qual se conectar. Por padrão, é exibida a instância de servidor usada na última conexão.  
  
**Autenticação**  
A versão atual do SSMS oferece cinco modos de autenticação ao conectar-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)]. Se a caixa de diálogo Autenticação não corresponder à lista a seguir, baixe a versão mais recente do SSMS em [Baixar o SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md).     
  
Ao conectar-se a uma instância do Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio do [!INCLUDE[ssSDS](../../includes/sssds-md.md)], você deve usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e especificar um banco de dados na caixa de diálogo **Conectar ao Servidor** , na guia **Propriedades da Conexão** . Verifique se você marcou a caixa de seleção **Criptografar conexão** .  
  
Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conecta-se ao **mestre**. Se você especificar um banco de dados de usuário ao se conectar ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)], somente esse banco de dados e seus objetos serão exibidos no Pesquisador de Objetos. Se você se conectar ao **mestre**, todos os bancos de dados serão exibidos. Confira mais informações em [Visão geral do Banco de Dados SQL do Microsoft Azure](/azure/sql-database/sql-database-technical-overview/).  
  
> **Autenticação do Windows**  
> [!INCLUDE[msCoName](../../includes/msconame_md.md)] O modo de Autenticação do Windows permite que um usuário se conecte por uma conta de usuário Windows.  
> 
> **Autenticação do SQL Server**  
> Quando um usuário se conecta com um nome de logon e uma senha especificados em uma conexão não confiável, o próprio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] efetua a autenticação verificando se foi definida uma conta de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e se a senha especificada corresponde a uma senha já registrada. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tiver uma conta de logon definida, ocorrerá falha na autenticação e o usuário receberá uma mensagem de erro. Quando possível, use a Autenticação do Windows.  
> 
> **Active Directory – Universal com suporte do MFA**  
> Active Directory – Universal com MFA é um fluxo de trabalho interativo que dá suporte à MFA (Autenticação Multifator do Azure). A MFA do Azure ajuda a proteger o acesso a dados e aplicativos enquanto atende à demanda do usuário para um processo de entrada simples. Ela fornece autenticação forte com uma variedade de opções de verificação fácil (chamada telefônica, mensagem de texto, cartões inteligentes com PIN ou notificação por aplicativos móveis) permitindo que os usuários escolham o método que preferirem. Quando a conta de usuário é configurada para MFA, o fluxo de trabalho de autenticação interativa requer interação adicional do usuário por meio de caixas de diálogo pop-up, uso de cartão inteligente etc. Quando a conta de usuário é configurada para MFA, o usuário deve selecionar Autenticação Universal do Azure para se conectar. Se a conta de usuário não exigir MFA, o usuário ainda poderá usar as outras duas opções de Autenticação do Azure Active Directory. Para obter mais informações, consulte [Suporte ao SSMS para MFA do Azure AD com o banco de dados SQL e o SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). Se necessário, você pode alterar o domínio que autentica o logon, clicando em **Opções**, selecionando guia **Propriedades de Conexão** e, em seguida, preenchendo a caixa **ID de locatário ou de nome de domínio do AD**.  
> 
> **Active Directory – Senha**  
> A Autenticação do Azure Active Directory é um mecanismo para se conectar ao [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] usando identidades no Azure AD (Azure Active Directory).  Use esse método para conectar-se ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)] se você tiver feito logon no Windows usando as credenciais de um domínio que não seja federado ao Azure ou usando a autenticação do Azure AD usando o Azure AD com base no domínio inicial ou do cliente. Para obter mais informações, veja [Conectar-se ao Banco de Dados SQL usando a Autenticação do Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
> 
> **Active Directory – Integrado**  
> A Autenticação do Azure Active Directory é um mecanismo para se conectar ao [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] usando identidades no Azure AD (Azure Active Directory). Use esse método para conectar-se ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)] se você tiver feito logon no Windows usando suas credenciais do Azure Active Directory de um domínio federado. Para obter mais informações, veja [Conectar-se ao Banco de Dados SQL usando a Autenticação do Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
**User name**  
O nome de usuário Windows com o qual se conectar. Essa opção estará disponível somente se você decidiu se conectar usando a **Autenticação da Senha do Active Directory**. Ele é somente leitura quando você seleciona a **Autenticação do Windows** ou a autenticação do **Active Directory – Integrado**.  
  
**Logon**  
Insira o logon com o qual se conectar. Essa opção estará disponível somente se você tiver decidido se conectar usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou a Autenticação de Senha do Active Directory.  
  
**Senha**  
Digite a senha do logon. Essa opção estará editável somente se você tiver decidido se conectar usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou a Autenticação de Senha do Active Directory.  
  
**Lembrar senha**  
Clique para que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazene a senha que você digitou. Essa opção só será exibida se você tiver optado por conectar-se usando a autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**Connect**  
Clique para conectar-se ao servidor.  
  
**Opções**  
Clique para exibir as guias **Propriedades de Conexão** e **Parâmetros Adicionais de Conexão**.  
   
  
