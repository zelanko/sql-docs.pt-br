---
title: "Conectar ao Mecanismo de Banco de Dados do Servidor (página Logon) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1556c7facc4a671767fe2d6c061b4f6655ba521b
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-login-page-database-engine"></a>Conectar ao Servidor (página Logon) Mecanismo de Banco de Dados
Use essa guia para exibir ou especificar opções ao se conectar ao [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)].  
  
> [!NOTE]  
> Para se conectar usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] deverá ser configurado no modo de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e do Windows. Para obter mais informações sobre como determinar o modo de autenticação e para alterar esse modo, consulte [Como alterar o modo de autenticação do servidor](http://msdn.microsoft.com/en-us/79babcf8-19fd-4495-b8eb-453dc575cac0).  
  
## <a name="options"></a>Opções  
**Tipo de servidor**  
Ao registrar um servidor a partir do Pesquisador de Objetos, selecione o tipo de servidor ao qual se conectar: [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services ou Integration Services. O restante da caixa de diálogo mostra somente as opções que se aplicam ao tipo de servidor selecionado. Ao registrar um servidor de Servidores Registrados, a caixa **Tipo de servidor** é somente leitura e corresponde ao tipo de servidor exibido no componente Servidores Registrados. Para registrar outro tipo de servidor, selecione [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services ou Integration Services na barra de ferramentas Servidores Registrados antes de iniciar o registro de um novo servidor.  
  
Ao conectar-se a uma instância do Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] por meio do [!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)], você deve usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e especificar um banco de dados na caixa de diálogo **Conectar ao Servidor** , na guia **Propriedades da Conexão** . Verifique se você marcou a caixa de seleção **Criptografar conexão** .  
  
Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] conecta-se ao **mestre**. Se você especificar um banco de dados de usuário, consultará somente esse banco de dados e seus objetos no Pesquisador de Objetos. Se você se conectar ao **mestre**, poderá ver todos os bancos de dados. Para obter mais informações, consulte [Visão geral do banco de dados SQL do Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=163948).  
  
**Nome do servidor**  
Selecione a instância do servidor com a qual se conectar. Por padrão, é exibida a instância de servidor usada na última conexão.  
  
**Autenticação**  
Dois modos de autenticação estão disponíveis quando se estabelece conexão com uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)].  
  
Ao conectar-se a uma instância do Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] por meio do [!INCLUDE[ssSDS](../../includes/sssds_md.md)], você deve usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e especificar um banco de dados na caixa de diálogo **Conectar ao Servidor** , na guia **Propriedades da Conexão** . Verifique se você marcou a caixa de seleção **Criptografar conexão** .  
  
Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] conecta-se ao **mestre**. Se você especificar um banco de dados de usuário, consultará somente esse banco de dados e seus objetos no Pesquisador de Objetos. Se você se conectar ao **mestre**, poderá ver todos os bancos de dados. Para obter mais informações, consulte [Visão geral do banco de dados SQL do Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=163948).  
  
**Autenticação do Windows**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] O modo de Autenticação do Windows permite que um usuário se conecte por uma conta de usuário Windows.  
  
**Autenticação do SQL Server**  
Quando um usuário se conecta com um nome de logon e uma senha especificados em uma conexão não confiável, o próprio [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] efetua a autenticação verificando se foi definida uma conta de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e se a senha especificada corresponde a uma senha já registrada. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] não tiver uma conta de logon definida, ocorrerá falha na autenticação e o usuário receberá uma mensagem de erro.  
  
> [!IMPORTANT]  
> Quando possível, use a Autenticação do Windows.  
  
**Autenticação Universal do Active Directory**  
A Autenticação Universal do Active Directory é um fluxo de trabalho interativo que dá suporte à MFA (Autenticação Multifator do Azure). A MFA do Azure ajuda a proteger o acesso a dados e aplicativos enquanto atende à demanda do usuário para um processo de entrada simples. Ela fornece autenticação forte com uma variedade de opções de verificação fácil – chamada telefônica, mensagem de texto, cartões inteligentes com PIN ou notificação por aplicativos móveis – permitindo que os usuários escolham o método que preferirem. Quando a conta de usuário é configurada para MFA, o fluxo de trabalho de autenticação interativa requer interação adicional do usuário por meio de caixas de diálogo pop-up, uso de cartão inteligente etc. Quando a conta de usuário é configurada para MFA, o usuário deve selecionar Autenticação Universal do Azure para se conectar. Se a conta de usuário não exigir MFA, o usuário ainda poderá usar as outras duas opções de Autenticação do Azure Active Directory. Para obter mais informações, consulte [Suporte ao SSMS para MFA do Azure AD com o banco de dados SQL e o SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). Requer pelo menos o SSMS versão 16.3 (agosto de 2016).
  
**Autenticação da Senha do Active Directory**  
A Autenticação do Azure Active Directory é um mecanismo para se conectar ao [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] usando identidades no Azure AD (Azure Active Directory).  Use esse método para se conectar ao [!INCLUDE[ssSDS](../../includes/sssds_md.md)] se você fez logon no Windows usando as credenciais de um domínio que não é federado com o Azure ou usando a autenticação do Azure AD usando o Azure AD com base no domínio inicial ou do cliente. Para obter mais informações, veja [Conectar-se ao Banco de Dados SQL usando a Autenticação do Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
**Autenticação Integrada do Active Directory**  
A Autenticação do Azure Active Directory é um mecanismo para se conectar ao [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] usando identidades no Azure AD (Azure Active Directory). Use esse método para se conectar ao [!INCLUDE[ssSDS](../../includes/sssds_md.md)] se você fez logon no Windows usando suas credenciais do Azure Active Directory de um domínio federado. Para obter mais informações, veja [Conectar-se ao Banco de Dados SQL usando a Autenticação do Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
**Nome de usuário**  
O nome de usuário Windows com o qual se conectar. Essa opção estará disponível somente se você decidiu se conectar usando a **Autenticação da Senha do Active Directory**. Ela é somente leitura quando você selecionar **Autenticação do Windows**.  
  
**Logon**  
Insira o logon com o qual se conectar. Essa opção estará disponível somente se você decidiu conectar-se usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
**Senha**  
Digite a senha do logon. Essa opção poderá ser editada somente se você decidiu conectar-se usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
**Lembrar senha**  
Clique para que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] armazene a senha que você digitou. Essa opção só será exibida se você tiver optado por conectar-se usando a autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
**Conectar**  
Clique para conectar-se com o servidor selecionado acima.  
  
**Opções**  
Clique para alterar a caixa de diálogo e ocultar as opções de conexão de servidor adicionais, como lembrar a senha.  
  

