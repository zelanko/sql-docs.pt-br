---
title: Configuração de Mecanismo de Banco de Dados – provisionamento de conta | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 834b26bc-49de-4033-88d5-6aa7b1609720
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 300e3dd81ae7a3de2361c79864130c1361c19588
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66095867"
---
# <a name="database-engine-configuration---account-provisioning"></a>Configuração do Mecanismo de Banco de Dados – Provisionamento de conta
  Use esta página para definir o modo de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e adicionar grupos ou usuários do Windows como administradores do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
## <a name="considerations-for-running-includesscurrentincludessscurrent-mdmd"></a>Considerações sobre execução do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o grupo **BUILTIN\Administradores** era provisionado como um logon no [!INCLUDE[ssDE](../../includes/ssde-md.md)] e os membros do grupo local Administradores podiam fazer logon usando as credenciais de Administrador. O uso de permissões elevadas não é uma prática recomendada. No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , o grupo **BUILTIN\Administradores** não é provisionado como logon. Por isso, você deve criar um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cada usuário administrativo e adicionar esse logon à função de servidor fixa sysadmin durante a instalação de uma nova instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Você também deve fazer isso para as contas do Windows usadas para executar trabalhos de agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Eles incluem trabalhos do agente de replicação.  
  
## <a name="options"></a>Opções  
 **Modo de segurança** – selecione Autenticação do Windows ou autenticação de modo misto para a instalação.  
  
 **Provisionamento de entidade de segurança do Windows** -em versões [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]anteriores do, o grupo local do Windows Builtin\Administrator foi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] colocado na função de servidor sysadmin, concedendo efetivamente acesso de administradores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Windows à instância do. No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o grupo Builtin\Administradores não é provisionado na função de servidor sysadmin. Em vez disso, você deve provisionar explicitamente administradores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para as novas instalações durante a Instalação.  
  
> [!IMPORTANT]  
>  Você deve provisionar explicitamente administradores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para as novas instalações durante a Instalação. A Instalação não permitirá que você continue até que conclua esta etapa.  
  
 **Especificar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administradores** – você deve especificar pelo menos uma entidade de segurança do Windows para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a instância do. Para adicionar a conta sob a qual a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada, clique no botão **Usuário Atual** . Para adicionar ou remover contas da lista de administradores do sistema, clique em **Adicionar** ou **Remover**e edite a lista de usuários, grupos ou computadores que terão privilégios de administrador para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Depois de concluir a edição da lista, clique em **OK**e verifique a lista de administradores na caixa de diálogo de configuração. Quando a lista estiver concluída, clique em **Avançar**.  
  
 Se você selecionar Autenticação de Modo Misto, deverá fornecer credenciais de logon para a conta interna AS (administrador do sistema) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 **Modo de autenticação do Windows**  
 Quando um usuário se conecta por uma conta de usuário do Windows, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valida o nome e a senha da conta usando o token da entidade do Windows no sistema operacional. Este é o modo de autenticação padrão e é muito mais seguro que o Modo Misto. A Autenticação do Windows usa o protocolo de segurança Kerberos, fornece imposição de política de senha e termos de validação de complexidade para senhas fortes, dá suporte ao bloqueio de contas e dá suporte à expiração de senhas.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]Nunca defina uma senha SA em branco ou fraca.  
  
 **Modo misto (autenticação do Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou autenticação)**  
 Permite que os usuários se conectem usando Autenticação do Windows ou Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os usuários que se conectarem por uma conta de usuário do Windows podem usar conexões confiáveis que são validadas pelo Windows.  
  
 Se você deve escolher Autenticação de Modo Misto e tem um requisito para usar logons do SQL a fim de acomodar aplicativos herdados, deverá definir senhas fortes para todas as contas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]A autenticação é fornecida apenas para fins de compatibilidade com versões anteriores. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 **Inserir senha**  
 Insira e confirme o logon de administrador de sistema (sa). As senhas são a primeira linha de defesa contra intrusos; portanto, a configuração de senhas fortes é essencial para a segurança do seu sistema. Nunca defina uma senha de sa em branco ou fraca.  
  
> [!NOTE]  
>  Senhas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem conter de 1 até 128 caracteres, incluindo qualquer combinação de letras, símbolos e números. Se você escolher a autenticação de Modo Misto, deverá inserir uma senha forte de sa antes de continuar na próxima página do Assistente de Instalação.  
  
 **Diretrizes de senha forte**  
 As senhas fortes não são prontamente adivinhadas por uma pessoa e não são facilmente violadas usando-se um programa de computador. As senhas fortes não podem usar condições ou termos proibidos, incluindo:  
  
-   Um espaço em branco ou condição NULL  
  
-   "Password"  
  
-   "Admin"  
  
-   "Administrador"  
  
-   "sa"  
  
-   "sysadmin"  
  
 Uma senha forte não pode ter os termos a seguir associados ao computador de instalação:  
  
-   O nome do usuário atualmente conectado à máquina.  
  
-   O nome do computador.  
  
 Uma senha forte deve ter mais de 8 caracteres e satisfazer pelo menos três dos quatro critérios a seguir:  
  
-   Deve conter letras maiúsculas.  
  
-   Deve conter letras minúsculas.  
  
-   Deve conter números.  
  
-   Deve conter caracteres não alfanuméricos; por exemplo, #,% ou ^.  
  
 As senhas inseridas nessa página devem satisfazer os requisitos de política de senha forte. Se você tiver qualquer automação que use Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , assegure-se de que a senha satisfaça os requisitos de política de senha forte.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Para obter mais informações sobre como escolher a Autenticação do Windows vs. Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , veja o tópico **Escolher um Modo de Autenticação** nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para obter mais informações sobre como escolher uma conta para executar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], consulte o tópico **Configurar contas de serviço e permissões do Windows** nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
