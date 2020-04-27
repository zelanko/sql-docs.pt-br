---
title: Definir a conta de serviço para o Iniciador do Daemon de Filtro de Texto Completo | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], FDHOST Launcher (MSSQLFDLauncher) service account
- FDHOST Launcher (MSSQLFDLauncher) [SQL Server]
ms.assetid: 3ab1d101-7ae0-488f-9b57-468e2517b737
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8f327cefbb916bf83f695db40a1d3c3025b7a5d2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66010944"
---
# <a name="set-the-service-account-for-the-full-text-filter-daemon-launcher"></a>Definir a conta de serviço do Iniciador do Daemon de Filtro de Texto Completo
  Este tópico descreve como definir a conta do serviço Iniciador do Daemon de Filtro de Texto Completo do SQL (MSSQLFDLauncher) usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. O serviço Iniciador do Daemon do Filtro de Texto Completo do SQL é usado pela pesquisa de texto completo ssNoVersion para iniciar o processo do host do daemon de filtro, que manipula a filtragem da pesquisa de texto completo e a quebra de palavras. Esse serviço deve estar em execução para usar a pesquisa de texto completo.  
  
 O Iniciador do Daemon de Filtro de Texto Completo do SQL é um serviço de reconhecimento de instâncias associado a uma instância específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O serviço Iniciador do Daemon de Filtro de Texto Completo do SQL propaga as informações da conta de serviço para cada processo do host do daemon de filtro.  
  
  
##  <a name="setting-the-service-account"></a><a name="setting"></a>Configurando a conta de serviço  
  
#### <a name="to-set-the-sql-full-text-filter-daemon-launcher-service-account-for-full-text-search"></a>Para definir a conta do serviço Iniciador do Daemon de Filtro de Texto Completo do SQL para pesquisa de texto completo  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
2.  Em **SQL Server Configuration Manager**, clique em **serviços SQL Server**, clique com o botão direito do mouse em ***`instance name`* iniciador do daemon de filtro de texto completo do SQL ()** e clique em **Propriedades**.  
  
3.  Clique na guia **Fazer Logon** da caixa de diálogo e selecione ou digite a conta em que será executado cada processo criado pelo serviço Iniciador do Daemon de Filtro de Texto Completo do SQL.  
  
4.  Depois que você fechar a caixa de diálogo, clique em **Reiniciar** para reiniciar o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL.  
  
  
##  <a name="if-the-sql-full-text-filter-daemon-launcher-service-does-not-start"></a><a name="error"></a>Se o serviço de Iniciador do Daemon de Filtro de Texto Completo do SQL não iniciar  
 Se o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL não for iniciado, o motivo poderá ser uma ou mais das seguintes condições:  
  
-   A senha associada à conta do serviço Iniciador do Daemon de Filtro de Texto Completo do SQL expirou.  
  
     Se você utiliza uma conta de usuário local para o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL e a senha expirar, será necessário.  
  
    1.  Definir uma nova senha do Windows para a conta.  
  
    2.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, atualize o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL para usar a nova senha.  
  
-   A conta de usuário ou a senha da conta de serviço está incorreta.  
  
     O serviço Iniciador do Daemon de Filtro de Texto Completo do SQL pode tentar fazer logon com uma conta de usuário e senha incorretas. Siga os procedimentos anteriores para verificar se a conta de usuário para o serviço não foi alterada.  
  
-   A conta usada para fazer logon no serviço não possui privilégios.  
  
     Talvez você esteja usando uma conta que não possui privilégios de logon no computador em que está instalada a instância do servidor. Verifique se está fazendo o logon com uma conta que possua direitos e permissões de Usuário no computador local.  
  
-   Outra instância do mesmo pipe nomeado já está sendo executada.  
  
     Os serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atua como um servidor de pipe nomeado para o cliente do serviço Iniciador do Daemon de Filtro de Texto Completo do SQL. Se o pipe nomeado já foi criado por outro processo antes de o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ser iniciado, um erro será registrado no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e no Log de Eventos do Windows, e a pesquisa de texto completo não estará disponível.  Determine qual processo ou aplicativo está tentando usar o mesmo pipe nomeado e interrompa o aplicativo.  
  
-   O serviço Iniciador do Daemon de Filtro de Texto Completo do SQL não está configurado corretamente.  
  
     O serviço pode não estar configurado corretamente no computador local.  
  
     Se a funcionalidade de pipes nomeados foi desabilitada no computador local ou se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi configurado para usar um pipe nomeado diferente do padrão, é possível que o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL não seja iniciado.  
  
-   O grupo de serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tem permissão para iniciar o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL.  
  
     Durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é concedido ao grupo de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permissão padrão para gerenciar, consultar e iniciar o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL. Se as permissões do grupo de serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a conta de serviço Iniciador do Daemon de Filtro de Texto Completo do SQL tiverem sido removidas após a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL não será iniciado e a pesquisa de texto completo será desabilitada. Certifique-se de que o grupo de serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenha permissões na conta de serviço Iniciador do Daemon de Filtro de Texto Completo do SQL.  
  
  
## <a name="see-also"></a>Consulte Também  
 [Tópicos de instruções sobre gerenciamento de serviços &#40;SQL Server Configuration Manager&#41;](../../database-engine/managing-services-how-to-topics-sql-server-configuration-manager.md)  
 [Atualizar pesquisa de texto completo](upgrade-full-text-search.md)  
  
  
