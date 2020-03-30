---
title: 'Instalar ferramentas de cliente: cluster de failover'
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.reviewer: ''
ms.prod: sql
ms.technology: install
ms.topic: conceptual
ms.assetid: 3c82d510-9798-46be-bebb-cac9bef56936
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c4918cdbb99a49bf577f9efad19ed0360c9a4911
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75230496"
---
# <a name="install-client-tools-on-a-sql-server-failover-cluster"></a>Instalar as ferramentas de cliente em um cluster de failover do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  As ferramentas de cliente, como o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , são recursos comuns compartilhados por todas as instâncias no mesmo computador. Elas são compatíveis com versões anteriores, com suporte para versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que podem ser instaladas lado a lado. Em um nó, existe somente uma versão por vez da ferramenta de cliente.  
  
 Se as ferramentas de cliente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] forem instaladas durante instalação no primeiro nó do cluster do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , elas serão adicionadas automaticamente a qualquer nó que possa ser adicionado posteriormente à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com o recurso Adicionar Nó.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Os Manuais Online não são automaticamente adicionados aos nós adicionais incluídos no cluster do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com o recurso Adicionar Nó. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Os Manuais Online podem ser instalados manualmente nos nós que você deseja que tenham uma cópia local dos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Se você não instalar as ferramentas de cliente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] durante a instalação inicial do cluster do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , poderá instalá-las posteriormente conforme descrito nos procedimentos a seguir.  
  
## <a name="installation-procedures"></a>Procedimentos de instalação  
  
#### <a name="installing-ssnoversion-client-tools-using-the-setup-user-interface"></a>Instalando as ferramentas de cliente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a interface do usuário da Instalação  
  
1.  Insira a mídia de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Na pasta de instalação raiz, clique duas vezes em Setup.exe. Para instalar a partir do compartilhamento de rede, localize a pasta raiz no compartilhamento e clique duas vezes em Setup.exe.  
  
2.  Na página **Instalação**, clique em **Nova instalação autônoma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou adicionar recursos a uma instalação existente**. Não clique em **Nova instalação de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]** .  
  
3.  O Verificador de Configuração do Sistema verifica o estado do sistema do computador antes de a Instalação continuar.  
  
4.  Na página **Tipo de Instalação**, clique em **Executar uma nova instalação do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]** .  
  
5.  Na página **Seleção de Recursos** , selecione as ferramentas que deseja instalar e execute as etapas restantes do processo de Instalação.  
  
#### <a name="installing-ssnoversion-client-tools-at-the-command-prompt"></a>Instalando as ferramentas de cliente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no prompt de comando  
  
1.  Para instalar ferramentas de cliente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e os Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], execute o seguinte comando: Setup.exe/q/Action=Install /Features=Tools  
  
2.  Para instalar somente as ferramentas básicas de Gerenciamento do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], execute o seguinte comando: Setup.exe/q/Action=Install Features=SSMS. Isso instalará o suporte do [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] para o [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)], o [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)], o utilitário sqlcmd e o provedor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell.  
  
3.  Para instalar as ferramentas completas de Gerenciamento do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], execute o seguinte comando: Setup.exe/q/Action=Install /Features=ADV_SSMS. Para obter mais informações sobre valores de parâmetro para os recursos, consulte [Instalar o SQL Server 2016 do prompt de comando](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
### <a name="uninstalling-ssnoversion-client-tools"></a>Desinstalando as ferramentas de cliente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 Elas aparecem em Adicionar ou Remover Programas, no Painel de controle, como **[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]** e podem ser removidas de lá. Quando você usa Remover Nó para desinstalar uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do cluster de failover, os componentes de cliente não são desinstalados ao mesmo tempo.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
