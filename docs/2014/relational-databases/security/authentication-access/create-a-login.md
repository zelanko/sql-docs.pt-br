---
title: Criar um logon | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.LOGIN.SERVERROLES.F1
- sql12.swb.login.databaseaccess.f1
- sql12.swb.login.general.f1
- sql12.swb.login.effectivepermissions.f1
- sql12.swb.login.status.f1
helpviewer_keywords:
- authentication [SQL Server], logins
- logins [SQL Server], creating
- creating logins with Management Studio
- Create login [SQL Server]
- SQL Server logins
ms.assetid: fb163e47-1546-4682-abaa-8c9494e9ddc7
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: b765248e43dc66b9e1c038df27ca9a8b6135706d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63012024"
---
# <a name="create-a-login"></a>Crie um logon
  Este tópico descreve como criar um logon no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Um logon é a identidade da pessoa ou do processo que está se conectando a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Plano de fundo](#Background)  
  
     [Segurança](#Security)  
  
-   **Para criar um logon, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [Etapas a serem executadas após criar um logon](#FollowUp)  
  
##  <a name="Background"></a> Plano de fundo  
 Um logon é uma entidade de segurança ou uma entidade que pode ser autenticada por um sistema seguro. Usuários precisam de um logon para se conectar ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Você pode criar um logon com base em uma entidade de segurança do Windows (como um usuário de domínio ou um grupo de domínio do Windows) ou pode criar um logon que não esteja baseado em uma entidade de segurança do Windows (como um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ).  
  
> [!NOTE]  
>  Para usar a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] deve usar a autenticação de modo misto. Para obter mais informações, veja [Escolher um modo de autenticação](../choose-an-authentication-mode.md).  
  
 Como uma entidade de segurança, as permissões podem ser concedidas a logons. O escopo de um logon é o [!INCLUDE[ssDE](../../../includes/ssde-md.md)]inteiro. Para se conectar a um banco de dados específico na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], um logon deve ser mapeado para um usuário de banco de dados. Permissões, e não o logon, são concedidas dentro do banco de dados e são negadas ao usuário de banco de dados. Permissões que têm o escopo da instância inteira do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (por exemplo, a permissão `CREATE ENDPOINT`) podem ser concedidas a um logon.  
  
##  <a name="Security"></a> Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão `ALTER ANY LOGIN` ou `ALTER LOGIN` no servidor.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
##### <a name="to-create-a-sql-server-login"></a>Para criar um logon do SQL Server  
  
1.  No Pesquisador de Objetos, expanda a pasta da instância de servidor no qual deseja criar o novo logon.  
  
2.  Clique com o botão direito do mouse na pasta **Segurança**, aponte para **Novo** e selecione **Logon...**.  
  
3.  Na caixa de diálogo **Logon – Novo**, na página **Geral**, insira o nome de um usuário na caixa **Nome de logon**. Como alternativa, clique em **Pesquisar...** para abrir a caixa de diálogo **Selecionar Usuário ou Grupo**.  
  
     Se você clicar em **Pesquisar...**:  
  
    1.  Em **Selecionar este tipo de objeto**, clique em **Tipos de Objeto...** para abrir a caixa de diálogo **Tipos de Objeto** e selecione uma ou todas as seguintes opções: **Entidades de segurança internas**, **Grupos** e **Usuários**. **Entidades de segurança internas** e **Usuários** estão selecionados por padrão. Quando terminar, clique em **OK**.  
  
    2.  Em **Desta localização**, clique em **Localizações...** para abrir a caixa de diálogo **Localizações** e selecione um dos locais de servidor disponíveis. Quando terminar, clique em **OK**.  
  
    3.  Sob **Inserir os nomes de objeto a serem selecionados (exemplos)**, insira o nome de usuário ou de grupo que você deseja localizar. Para obter mais informações, consulte [Caixa de Diálogo Selecionar Usuários, Computadores ou Grupos](https://technet.microsoft.com/library/cc771712.aspx).  
  
    4.  Clique em **Avançado...** para mais opções de pesquisa avançada. Para obter mais informações, veja [Caixa de Diálogo Selecionar Usuários, Computadores ou Grupos – Página Avançada](https://technet.microsoft.com/library/cc733110.aspx).  
  
    5.  Clique em **OK**.  
  
4.  Para criar um logon fundado em uma entidade de segurança de Windows, selecione **Autenticação do Windows**. Essa é a seleção padrão.  
  
5.  Para criar um logon salvo em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , selecione **Autenticação do SQL Server**.  
  
    1.  Na caixa **Senha** , digite uma senha para o novo usuário. Digite essa senha novamente na caixa **Confirmar Senha** .  
  
    2.  Ao alterar uma senha existente, selecione **Especificar senha antiga**e digite a senha antiga na caixa **Senha antiga** .  
  
    3.  Para impor opções de política de senha para complexidade e execução, selecione **Impor política de senha**. Para obter mais informações, consulte [Password Policy](../password-policy.md). Esta será uma opção padrão quando **Autenticação do SQL Server** estiver selecionada.  
  
    4.  Para impor opções de política de senha para expiração, selecione **Impor expiração de senha**. **Impor política de senha** deve ser selecionada para habilitar esta caixa de seleção. Esta será uma opção padrão quando **Autenticação do SQL Server** estiver selecionada.  
  
    5.  Para forçar o usuário a criar uma nova senha depois da primeira vez que o logon for usado, selecione **O usuário deve alterar senha a próximo logon**. **Impor expiração de senha** deve ser selecionada para habilitar esta caixa de seleção. Esta será uma opção padrão quando **Autenticação do SQL Server** estiver selecionada.  
  
6.  Para associar o logon a um certificado de segurança autônomo, selecione **Mapeado para certificado** e selecione o nome de um certificado existente na lista.  
  
7.  Para associar o logon a uma chave assimétrica autônoma, selecione **Mapeado para chave assimétrica** e selecione o nome de uma chave existente na lista.  
  
8.  Para associar o logon a uma credencial de segurança, marque a caixa de seleção **Mapeado para Credencial** e então selecione uma credencial existente na lista ou clique em **Adicionar** para criar uma nova credencial. Para remover um mapeamento a uma credencial de segurança do logon, selecione a credencial de **Credenciais Mapeadas** e clique em **Remover**. Para obter mais informações sobre credenciais em geral, veja [Credenciais &#40;Mecanismo de Banco de Dados&#41;](credentials-database-engine.md).  
  
9. Na lista **Banco de dados padrão** , selecione um banco de dados padrão para o logon. **Master** é o padrão dessa opção.  
  
10. Na lista **Idioma padrão** , selecione um idioma padrão para o logon.  
  
11. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>Opções adicionais  
 A caixa de diálogo **Logon – Novo** também oferece opções em quatro páginas adicionais: **Funções de Servidor**, **Mapeamento de Usuário**, **Protegíveis** e **Status**.  
  
### <a name="server-roles"></a>Funções de Servidor  
 A página **Funções de Servidor** lista todas as funções possíveis que podem ser atribuídas ao novo logon. As seguintes opções estão disponíveis:  
  
 Caixa de seleção**bulkadmin**   
 Os membros da função de servidor fixa **bulkadmin** podem executar a instrução BULK INSERT.  
  
 Caixa de seleção**dbcreator**   
 Os membros da função de servidor fixa **dbcreator** podem criar, alterar, remover e restaurar qualquer banco de dados.  
  
 Caixa de seleção**diskadmin**   
 Os membros da função de servidor fixa **diskadmin** podem gerenciar arquivos em disco.  
  
 Caixa de seleção**processadmin**   
 Os membros da função de servidor fixa **processadmin** podem encerrar processos em execução em uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
 Caixa de seleção**public**   
 Todos os usuários, grupos e funções do SQL Server pertencem à função de servidor fixa **public** .  
  
 Caixa de seleção**securityadmin**   
 Os membros da função de servidor fixa **securityadmin** gerenciam logons e suas propriedades. Eles podem CONCEDER, NEGAR e REVOGAR permissões de nível de servidor. Eles também podem CONCEDER, NEGAR e REVOGAR permissões de nível de banco de dados. Além disso, eles podem redefinir senhas para logons do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Caixa de seleção**serveradmin**   
 Os membros da função de servidor fixa **serveradmin** podem alterar as opções de configuração de todo o servidor e fechar o servidor.  
  
 Caixa de seleção**setupadmin**   
 Os membros da função de servidor fixa **setupadmin** podem adicionar e remover servidores vinculados e podem executar alguns procedimentos armazenados no sistema.  
  
 Caixa de seleção**sysadmin**   
 Os membros da função de servidor fixa **sysadmin** podem executar qualquer atividade no [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
### <a name="user-mapping"></a>Mapeamento de Usuário  
 A página **Mapeamento de Usuário** lista todos os possíveis bancos de dados e associações de função de banco de dados nesses bancos de dados que podem ser se aplicados ao logon. Os bancos de dados selecionados determinam as associações de função que estão disponíveis para o logon. As opções a seguir estão disponíveis nesta página:  
  
 **Usuários mapeados para este logon**  
 Selecione os bancos de dados que este logon pode acessar. Quando você seleciona um banco de dados, suas funções de banco de dados válidas são exibidas no painel **Associação à função de banco de dados para:** _database_name_ .  
  
 **Mapeamento**  
 Permita que o logon acesse os bancos de dados listados abaixo.  
  
 **Backup de banco de dados**  
 Liste os bancos de dados disponíveis no servidor.  
  
 **Usuário**  
 Especifique um usuário de banco de dados a ser mapeado para o logon. Por padrão, o usuário de banco de dados tem o mesmo nome do logon.  
  
 **Esquema Padrão**  
 Especifica o esquema padrão do usuário. Quando um usuário é criado pela primeira vez, seu esquema padrão é **dbo**. É possível especificar um esquema padrão que ainda não existe. Você não pode especificar um esquema padrão para um usuário mapeado para um grupo do Windows, um certificado ou uma chave assimétrica.  
  
 **Guest account enabled for:**  _database_name_  
 Atributo somente leitura que indica se a conta de Convidado está habilitada no banco de dados selecionado. Use a página **Status** da caixa de diálogo **Propriedades de Logon** da conta Convidado para habilitar ou desabilitar a conta Convidado.  
  
 **Database role membership for:**  _database_name_  
 Selecione as funções para o usuário no banco de dados especificado. Todos os usuários são membros da função **pública** em todo banco de dados e não podem ser removidos. Para obter mais informações sobre as funções de banco de dados, veja [Funções no nível de banco de dados](database-level-roles.md).  
  
### <a name="securables"></a>Protegíveis  
 A página **Protegíveis** lista todos os protegíveis e as permissões possíveis nesses protegíveis que podem ser concedidos ao logon. As opções a seguir estão disponíveis nesta página:  
  
 **Grade superior**  
 Contém um ou mais itens para os quais podem ser definidas permissões. As colunas que são exibidas na grade superior variam, dependendo da entidade ou protegível.  
  
 Para adicionar itens à grade superior:  
  
1.  Clique em **Pesquisar**.  
  
2.  Na caixa de diálogo **Adicionar Objetos**, selecione uma das seguintes opções: **Objetos específicos...** , **Todos os objetos dos tipos...** , ou **o servidor**_nome_do_servidor_. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  A seleção de **O servidor**_server_name_ preenche automaticamente a grade superior com os objetos protegíveis de todos os servidores.  
  
3.  Se você selecionar **Objetos específicos...**:  
  
    1.  Na caixa de diálogo **Selecionar Objetos**, em **Selecionar estes tipos de objeto**, clique em **Tipos de Objeto...**.  
  
    2.  Na caixa de diálogo **Selecionar Tipos de Objeto**, selecione um ou todos os seguintes tipos de objeto: **Pontos de extremidade**, **Logons**, **Servidores**, **Grupos de Disponibilidade** e **Funções de servidor**. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    3.  Em **Inserir os nomes de objeto a serem selecionados (exemplos)**, clique em **Procurar...**.  
  
    4.  Na caixa de diálogo **Procurar por Objetos** , selecione qualquer um dos objetos disponíveis do tipo que você selecionou na caixa de diálogo **Selecionar Tipos de Objeto** e então clique em **OK**.  
  
    5.  Na caixa de diálogo **Selecionar Objetos** , clique em **OK**.  
  
4.  Se você selecionar **Todos os objetos dos tipos...**, na caixa de diálogo **Selecionar Tipos de Objeto**, selecione um ou todos os seguintes tipos de objeto: **Pontos de extremidade**, **Logons**, **Servidores**, **Grupos de Disponibilidade** e **Funções de servidor**. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 **Nome**  
 O nome de cada entidade ou protegível que é adicionado à grade.  
  
 **Tipo**  
 Descreve o tipo de cada item.  
  
 **Guia Explícita**  
 Lista as permissões possíveis para o protegível que está selecionado na grade superior. Nem todas as opções estão disponíveis para todas as permissões explícitas.  
  
 **Permissões**  
 O nome da permissão.  
  
 **Concessor**  
 A entidade que concedeu a permissão.  
  
 **Conceder**  
 Selecione para conceder essa permissão ao logon. Desmarque para revogar essa permissão.  
  
 **Com Concessão**  
 Reflete o estado da opção WITH GRANT para a permissão listada. Essa caixa é somente leitura. Para aplicar essa permissão, use a instrução [GRANT](/sql/t-sql/statements/grant-transact-sql) .  
  
 **Deny**  
 Selecione para negar essa permissão ao logon. Desmarque para revogar essa permissão.  
  
### <a name="status"></a>Status  
 A página **Status** lista algumas das opções de autenticação e de autorização que podem ser configuradas no logo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] selecionado.  
  
 As opções a seguir estão disponíveis nesta página:  
  
 **Permissão para conexão com mecanismo de banco de dados**  
 Quando você trabalha nessa configuração, deve pensar no logon selecionado como uma entidade que pode ter a permissão concedida ou recusada em um protegível.  
  
 Selecione **Conceder** para conceder a permissão CONNECT SQL ao logon. Selecione **Negar** para negar CONNECT SQL ao logon.  
  
 **Logon**  
 Quando você trabalha nessa configuração, deve pensar no logon selecionado como um registro em uma tabela. As alterações dos valores listados aqui serão aplicadas ao registro.  
  
 Um logon que foi desabilitado continua existindo como um registro. Mas se tentar se conectar a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o logon não será autenticado.  
  
 Selecione esta opção para habilitar ou desabilitar o logon. Esta opção usa a instrução ALTER LOGON com a opção ENABLE ou DISABLE.  
  
 **SQL Server Authentication**  
 A caixa de seleção **O logon está bloqueado** só estará disponível se o logon selecionado se conectar usando a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e se estiver bloqueado. Esta configuração é somente leitura. Para desbloquear um logon bloqueado, execute ALTER LOGIN com a opção UNLOCK.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-login-using-windows-authentication"></a>Para criar um logon usando a Autenticação do Windows  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Create a login for SQL Server by specifying a server name and a Windows domain account name.  
  
    CREATE LOGIN [<domainName>\<loginName>] FROM WINDOWS;  
    GO  
  
    ```  
  
#### <a name="to-create-a-login-using-sql-server-authentication"></a>Para criar um logon usando a Autenticação do SQL Server  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Creates the user "shcooper" for SQL Server using the security credential "RestrictedFaculty"   
    -- The user login starts with the password "Baz1nga," but that password must be changed after the first login.  
  
    CREATE LOGIN shcooper   
       WITH PASSWORD = 'Baz1nga' MUST_CHANGE,  
       CREDENTIAL = RestrictedFaculty;  
    GO  
  
    ```  
  
 Para obter mais informações, veja [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql).  
  
##  <a name="FollowUp"></a> Acompanhamento: Etapas a serem executadas após criar um logon  
 Após ser criado, o logon pode se conectar ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], mas não necessariamente tem permissão suficiente para executar qualquer trabalho útil. A lista a seguir fornece links a ações de logon comuns.  
  
-   Para associar o logon a uma função, veja [Unir uma função](join-a-role.md).  
  
-   Para autorizar um logon a usar um banco de dados, veja [Criar um usuário de banco de dados](../authentication-access/create-a-database-user.md).  
  
-   Para conceder uma permissão a um logon, veja [Conceder uma permissão a uma entidade](grant-a-permission-to-a-principal.md).  
  
  
