---
title: "Configurar op&#231;&#245;es de inicializa&#231;&#227;o do servidor (SQL Server Configuration Manager) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "parâmetros [SQL Server], opções de inicialização"
  - "SQL Server, opções de inicialização"
  - "modo de usuário único [SQL Server], iniciando em"
  - "opções de inicialização [SQL Server]"
  - "Serviços do SQL Server, configurando opções de inicialização"
ms.assetid: 7a94643c-6460-4baf-bb31-0cb99eaf970d
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Configurar op&#231;&#245;es de inicializa&#231;&#227;o do servidor (SQL Server Configuration Manager)
  Este tópico descreve como configurar as opções de inicialização que serão usadas sempre que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] for iniciado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. Para obter uma lista de opções de inicialização, veja [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
### Limitações e restrições  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager grava parâmetros de inicialização no Registro. Eles entram em vigor na próxima vez que o [!INCLUDE[ssDE](../../includes/ssde-md.md)]for inicializado.  
  
 Em um cluster, as alterações devem ser feitas no servidor ativo quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está online, e entrarão em vigor quando o [!INCLUDE[ssDE](../../includes/ssde-md.md)] for reinicializado. A atualização do Registro das opções de inicialização no outro nó acontecerá no próximo failover.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 A configuração de opções de inicialização de servidor é restrita a usuários que podem alterar as entradas relacionadas no Registro. Isso inclui os seguintes usuários.  
  
-   Membros do grupo Administradores local.  
  
-   A conta de domínio usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] estiver configurado para ser executado em uma conta de domínio.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### Para configurar as opções de inicialização  
  
1.  Clique no botão **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], para **Ferramentas de Configuração**e, em seguida, clique em **SQL Server Configuration Manager**.  
  
    > [!NOTE]  
    >  Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager é um snap-in do programa Console de Gerenciamento [!INCLUDE[msCoName](../../includes/msconame-md.md)] e não um programa autônomo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager não aparece como um aplicativo nas versões mais recentes do Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, na **Página Inicial**, digite SQLServerManager13.msc (para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]). Para versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , substitua 13 por um número menor. Clicar em SQLServerManager13.msc abre o Configuration Manager. Para fixar o Configuration Manager na Página Inicial ou na Barra de Tarefas, clique com o botão direito do mouse em SQLServerManager13.msc e clique em **Abrir local do arquivo**. No Explorador de Arquivos do Windows, clique com o botão direito do mouse em SQLServerManager13.msc e clique em **Fixar na Tela Inicial** ou **Fixar na Barra de Tarefas**.  
    > -   **Windows 8**:  
    >          Para abrir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no botão **Pesquisar**, em **Aplicativos**, digite **SQLServerManager\<versão>.msc**, como **SQLServerManager13.msc**, e pressione **Enter**.  
  
2.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, clique em **Serviços do SQL Server**.  
  
3.  No painel direito, clique com o botão direito do mouse em **SQL Server (***<instance_name>***)** e clique em **Propriedades**.  
  
4.  Na guia **Parâmetros de Inicialização** , na caixa **Especificar um parâmetro de inicialização** , digite o parâmetro e clique em **Adicionar**.  
  
     Por exemplo, para iniciar um modo de usuário único, digite **-m** na caixa **Especificar um parâmetro de inicialização** e clique em **Adicionar**. (Ao reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único, interrompa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Caso contrário, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent poderá se conectar primeiro e impedir sua conexão como um segundo usuário.)  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Reinicie o [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
    > [!WARNING]  
    >  Ao terminar de usar o modo de usuário único, na caixa Parâmetros de Inicialização, selecione o parâmetro **-m** na caixa **Parâmetros Existentes** e clique em **Remover**. Reinicie o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para restaurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como o modo multiusuário típico.  
  
## Consulte também  
 [Iniciar o SQL Server no modo de usuário único](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)   
 [Conectar-se ao SQL Server quando os administradores do sistema estão bloqueados](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)   
 [Iniciar, parar ou pausar o serviço do SQL Server Agent](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  