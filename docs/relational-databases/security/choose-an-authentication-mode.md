---
title: Escolher um modo de autenticação | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.ins.instwizard.authenticationmode.f1
- sql13.swb.passwordexpired.f1
helpviewer_keywords:
- sa account
- authentication modes
- trusted connection
- SQL Server Installation Wizard, Authentication Mode page
- choose authentication mode
- authentication [SQL Server], choosing a mode
- Windows authentication [SQL Server]
- mixed mode authentication
- mixed authentication mode
- SQL authentication mode
- Password Expired dialog box
ms.assetid: ff7a6a48-3d38-4209-aa0f-7d6c0a8c64ef
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: ac0c3526439d0dc899e81554305c7602c4fa8a9d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781904"
---
# <a name="choose-an-authentication-mode"></a>Escolher um modo de autenticação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Durante a instalação, você deve selecionar um modo de autenticação para o [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Há dois modos possíveis: modo de Autenticação do Windows e modo misto. O modo de Autenticação do Windows habilita a Autenticação do Windows e desabilita a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O modo misto habilita a Autenticação do Windows e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A Autenticação do Windows sempre está disponível e não é possível desabilitá-la.  
  
## <a name="configuring-the-authentication-mode"></a>Configurando o modo de autenticação  
 Se você selecionar a Autenticação de Modo Misto durante a instalação, deverá fornecer e confirmar uma senha forte para a conta interna do administrador de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominada sa. A conta sa se conecta usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Se você selecionar a Autenticação do Windows durante a instalação, a Instalação criará a conta sa para a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mas ela ficará desabilitada. Se, depois você alterar para a Autenticação de Modo Misto e quiser usar a conta sa, será necessário habilitar essa conta. Qualquer conta do Windows ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser configurada como administrador do sistema. Como a conta sa é bem conhecida e, com frequência, visada por usuários mal-intencionados, não habilite a conta sa, a menos que o aplicativo solicite. Nunca defina uma senha em branco ou fraca para a conta sa. Para alterar do modo de Autenticação do Windows para a Autenticação de Modo Misto e usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , veja [Alterar modo de autenticação do servidor](../../database-engine/configure-windows/change-server-authentication-mode.md).  
  
## <a name="connecting-through-windows-authentication"></a>Conectando pela Autenticação do Windows  
 Quando um usuário se conecta por uma conta de usuário do Windows, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valida o nome e a senha da conta usando o token da entidade do Windows no sistema operacional. Isso significa que a identidade de usuário é confirmada pelo Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não solicita a senha e não executa a validação de identidade. A Autenticação do Windows é o modo de autenticação padrão e é muito mais segura do que a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A Autenticação do Windows usa o protocolo de segurança Kerberos, fornece imposição de política de senha em relação à validação de complexidade para senhas fortes, além de dar suporte ao bloqueio de contas e à expiração de senhas. Uma conexão estabelecida com uso da Autenticação do Windows às vezes é denominada conexão confiável, porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] confia nas credenciais fornecidas pelo Windows.  
  
 Usando a Autenticação do Windows, os grupos do Windows podem ser criados no nível de domínio, e um logon pode ser criado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para todo o grupo. Gerenciar o acesso no nível de domínio pode simplificar a administração da conta.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
## <a name="connecting-through-sql-server-authentication"></a>Conectando pela autenticação do SQL Server  
 Durante o uso da Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , são criados logons no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não se baseiam em contas de usuário do Windows. O nome de usuário e a senha são criados com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e armazenados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os usuários que se conectam com o uso da Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem fornecer suas credenciais (logon e senha) sempre que se conectarem. Ao usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você deve definir senhas fortes para todas as contas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter diretrizes de senha forte, veja [Senhas fortes](../../relational-databases/security/strong-passwords.md).  
  
 Três políticas de senha opcionais estão disponíveis para logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   O usuário deve alterar a senha no próximo logon  
  
     Requer que o usuário altere a senha o na próxima vez que se conectar. A capacidade de alterar a senha é fornecida pelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Os desenvolvedores de software de terceiros devem fornecer esse recurso se essa opção for usada.  
  
-   Impor vencimento de senha  
  
     A política de idade de senha máxima do computador é imposta para logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Impor política de senha  
  
     As políticas de senha do Windows do computador são impostas para logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Isso inclui comprimento e complexidade da senha. Essa funcionalidade depende da API `NetValidatePasswordPolicy` , disponível somente no [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] e nas versões posteriores.  
  
#### <a name="to-determine-the-password-policies-of-the-local-computer"></a>Para determinar as políticas de senha do computador local  
  
1.  No menu **Iniciar** , clique em **Executar**.  
  
2.  Na caixa de diálogo **Executar** , digite **secpol.msc**e clique em **OK**.  
  
3.  No aplicativo **Configurações de Segurança Local** , expanda **Configurações de Segurança**, **Políticas de Conta**e clique em **Política de Senha**.  
  
     As políticas de senha são descritas no painel de resultados.  
  
### <a name="disadvantages-of-sql-server-authentication"></a>Desvantagens da autenticação do SQL Server  
  
-   Se um usuário for usuário de domínio do Windows com logon e senha para o Windows, ele ainda deverá fornecer outras informações de logon e senha ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) para se conectar. Manter o controle de vários nomes e senhas é difícil para muitos usuários. Fornecer credenciais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cada conexão com o banco de dados pode ser um incômodo.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A Autenticação não pode usar o protocolo de segurança Kerberos.  
  
-   O Windows oferece políticas de senha adicionais que não estão disponíveis para logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   A senha criptografada do logon de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser transmitida pela rede no momento da conexão. Alguns aplicativos que se conectam automaticamente armazenarão a senha no cliente. Esses são pontos adicionais de ataque.  
  
### <a name="advantages-of-sql-server-authentication"></a>Vantagens da autenticação do SQL Server  
  
-   Permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dê suporte a aplicativos mais antigos e aplicativos fornecidos por terceiros que exigem a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dê suporte a ambientes com sistemas operacionais mistos, onde todos os usuários não são autenticados por um domínio do Windows.  
  
-   Permite que os usuários se conectem de domínios desconhecidos ou não confiáveis. Por exemplo, um aplicativo no qual os clientes estabelecidos se conectam com logons atribuídos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para receber o status das suas ordens.  
  
-   Permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dê suporte a aplicativos com base na Web em que os usuários criam suas próprias identidades.  
  
-   Permite que os desenvolvedores de software distribuam seus aplicativos com o uso de uma hierarquia de permissões complexa com base em logons predefinidos e conhecidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    > [!NOTE]  
    >  O uso da Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não limita as permissões dos administradores locais no computador em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado.  
  
## <a name="see-also"></a>Consulte Também  
 [Considerações sobre segurança para uma instalação do SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
