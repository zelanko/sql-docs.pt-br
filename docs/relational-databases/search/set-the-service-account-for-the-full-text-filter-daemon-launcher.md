---
title: "Definir a conta de servi&#231;o do Iniciador do Daemon de Filtro de Texto Completo | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "pesquisa de texto completo [SQL Server], conta de serviço do Iniciador FDHOST (MSSQLFDLauncher)"
  - "Iniciador FDHOST (MSSQLFDLauncher) [SQL Server]"
ms.assetid: 3ab1d101-7ae0-488f-9b57-468e2517b737
caps.latest.revision: 50
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 49
---
# Definir a conta de servi&#231;o do Iniciador do Daemon de Filtro de Texto Completo
  Este tópico descreve como definir a conta do serviço Iniciador do Daemon de Filtro de Texto Completo do SQL (MSSQLFDLauncher) usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. O serviço Iniciador do Daemon do Filtro de Texto Completo do SQL é usado pela pesquisa de texto completo ssNoVersion para iniciar o processo do host do daemon de filtro, que manipula a filtragem da pesquisa de texto completo e a quebra de palavras. Esse serviço deve estar em execução para usar a pesquisa de texto completo.  
  
 O Iniciador do Daemon de Filtro de Texto Completo do SQL é um serviço de reconhecimento de instâncias associado a uma instância específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O serviço Iniciador do Daemon de Filtro de Texto Completo do SQL propaga as informações da conta de serviço para cada processo do host do daemon de filtro.  
  
##  <a name="TOP"></a> Nesta seção  
  
-   [Recomendações de segurança](#rec)  
  
-   [Definindo a conta de serviço](#setting)  
  
-   [Se o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL não for iniciado](#error)  
  
##  <a name="setting"></a> Definindo a conta de serviço  
  
#### Para definir a conta do serviço Iniciador do Daemon de Filtro de Texto Completo do SQL para pesquisa de texto completo  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
2.  No **SQL Server Configuration Manager**, clique em **Serviços do SQL Server**, clique com o botão direito do mouse em **Iniciador do Daemon de Filtro de Texto Completo do SQL (***nome da instância***)** e clique em **Propriedades**.  
  
3.  Clique na guia **Fazer Logon** da caixa de diálogo e selecione ou digite a conta em que será executado cada processo criado pelo serviço Iniciador do Daemon de Filtro de Texto Completo do SQL.  
  
4.  Depois que você fechar a caixa de diálogo, clique em **Reiniciar** para reiniciar o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL.  
  
 [Nesta seção](#TOP)  
  
##  <a name="error"></a> Se o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL não for iniciado  
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
  
     Durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é concedido ao grupo de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permissão padrão para gerenciar, consultar e iniciar o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL. Se as permissões do grupo de serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a conta de serviço Iniciador do Daemon de Filtro de Texto Completo do SQL tiverem sido removidas após a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o serviço Iniciador do Daemon de Filtro de Texto Completo do SQL não será iniciado e a pesquisa de texto completo será desabilitada. Certifique-se de que o grupo de serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenha permissões na conta de serviço Iniciador do Daemon de Filtro de Texto Completo do SQL.  
  
 [Nesta seção](#TOP)  
  
## Consulte também  
 [Tópicos de instruções sobre gerenciamento de serviços &#40;SQL Server Configuration Manager&#41;](../Topic/Managing%20Services%20How-to%20Topics%20\(SQL%20Server%20Configuration%20Manager\).md)   
 [Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md)  
  
  