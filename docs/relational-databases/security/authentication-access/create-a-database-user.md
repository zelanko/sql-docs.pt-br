---
title: Criar um usuário de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.user.securables.f1
- SQL13.SWB.DATABASEUSER.GENERAL.F1
helpviewer_keywords:
- database users, creating
- creating users with Management Studio
- mapping users
- users [SQL Server], creating
- database user additions [SQL Server]
- database users, mapping
- CREATE USER [Management Studio]
- users [SQL Server], adding
- mapping database users
ms.assetid: 782798d3-9552-4514-9f58-e87be4b264e4
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3aa8e127c382d8f7915edbcb81e1272fe522251
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981936"
---
# <a name="create-a-database-user"></a>Criar um usuário de banco de dados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este tópico descreve como criar os tipos mais comuns de usuários de banco de dados. Há onze tipos de usuários. A lista completa é fornecida no tópico [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md). Todas as variedades de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dão suporte a usuários de banco de dados, mas não necessariamente todos os tipos de usuários.  
  
 Você pode criar um usuário de banco de dados usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
##  <a name="Understanding"></a> Noções básicas sobre os tipos de usuários  
 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] apresenta seis opções ao criar um usuário de banco de dados. O gráfico a seguir mostra as seis opções na caixa verde e indica o que elas representam.  
  
 ![TypesOfUsers](../../../relational-databases/security/authentication-access/media/typesofusers.png "TypesOfUsers")  
  
### <a name="selecting-the-type-of-user"></a>Selecionando o tipo de usuário  
 **Logon ou usuário que não está mapeado para um logon**  
  
 Se você ainda não conhece o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], pode ser difícil determinar que tipo de usuário deseja criar. Primeiro pergunte-se: a pessoa ou grupo que precisa acessar o banco de dados tem um logon? Os logons no banco de dados mestre são comuns para as pessoas que gerenciam o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e pessoas que precisam acessar muitos ou todos os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Nessa situação, você criará um **usuário do SQL com logon**. O usuário de banco de dados é a identidade do logon quando é conectado a um banco de dados. O usuário de banco de dados pode usar o mesmo nome como o logon, mas isso não é requerido. Este tópico pressupõe que já exista um logon no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações sobre como criar um logon, veja [Criar um logon](../../../relational-databases/security/authentication-access/create-a-login.md)  
  
 Se a pessoa ou grupo que precisa acessar o banco de dados não tiver um logon e se eles só precisarem de acesso para um ou alguns bancos de dados, crie um **usuário Windows** ou um **usuário do SQL com senha**. Também chamado de usuário de banco de dados independente, ele não está associado com logon no banco de dados mestre. Essa será uma excelente opção quando você quiser mover facilmente o banco de dados entre instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para usar essa opção no [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)], um administrador deve primeiro habilitar bancos de dados independentes para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], e o banco de dados deve ser habilitado para ser independente. Para obter mais informações, consulte [Usuários de bancos de dados independentes – Tornando seu banco de dados portátil](../../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
> **IMPORTANTE:** Ao conectar-se como um usuário de banco de dados independente, você deverá fornecer o nome do banco de dados como parte da cadeia de conexão. Para especificar o banco de dados no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], na caixa de diálogo **Conectar a** , clique em **Opções**e depois clique na guia **Propriedades de Conexão** .  
  
 Selecione **Usuário do SQL com senha** ou um **Usuário do SQL com logon** com base em um **logon de autenticação do SQL Server**, quando a pessoa que está conectada não pode autenticar com o Windows. Isso é comum quando as pessoas fora de sua organização (por exemplo, os clientes) estão se conectando ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
> **DICA!** Para as pessoas da sua organização, a autenticação do Windows é uma opção melhor, pois eles não precisam lembrar uma senha adicional e a autenticação do Windows oferece recursos de segurança adicionais, como o Kerberos.  
  
##  <a name="Restrictions"></a> Plano de fundo  
 Um usuário é uma entidade de segurança no nível de banco de dados. Logons devem ser mapeados para um usuário de banco de dados para ser conectados a um banco de dados. Um logon pode ser mapeado para bancos de dados diferentes como usuários diferentes, mas pode ser mapeado somente como um usuário em cada banco de dados. Em um banco de dados parcialmente independente, um usuário pode ser criado sem logon. Para obter mais informações sobre os usuários de banco de dados independente, veja [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md). Se o usuário convidado em um banco de dados estiver habilitado, um logon que não estiver mapeado para um usuário de banco de dados poderá acessar o banco de dados como um usuário convidado.  
  
> **IMPORTANTE:** O usuário convidado normalmente é desabilitado. Não habilite o usuário convidado, a menos que seja necessário.  
  
 Como uma entidade de segurança, permissões podem ser concedidas a usuários. O escopo de um usuário é o banco de dados. Para se conectar a um banco de dados específico na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], um logon deve ser mapeado para um usuário de banco de dados. Permissões, e não o logon, são concedidas dentro do banco de dados e são negadas ao usuário de banco de dados.  
  
##  <a name="Permissions"></a> Permissões  
 Requer a permissão **ALTER ANY USER** no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Criar um usuário com o SSMS  
  
 
1.  No Pesquisador de Objetos, expanda a pasta **Bancos de Dados** .  
  
2.  Expanda o banco de dados no qual o novo usuário de banco de dados será criado.  
  
3.  Clique com o botão direito do mouse na pasta **Segurança**, aponte para **Novo** e selecione **Usuário...** .  
  
4.  Na caixa de diálogo **Usuário de banco de dados – Novo** da página **Geral**, selecione um dos seguintes tipos de usuário na lista **Tipo de usuário**:  
  
    -   **usuário do SQL com logon**  
  
    -   **usuário do SQL com senha**  
  
    -   **Usuário do SQL sem logon**  
  
    -   **Usuário mapeado para um certificado**  
  
    -   **Usuário mapeado para uma chave assimétrica**  
  
    -   **usuário Windows**  
  
5.  Quando você seleciona uma opção, as opções restantes na caixa de diálogo podem ser alteradas. Algumas opções só se aplicam a tipos específicos de usuários de banco de dados. Algumas opções podem ser deixadas em branco e usarão o valor padrão.  
  
     **Nome de usuário**  
     Insira um nome para o novo usuário. Se você tiver escolhido **Usuário do Windows** na lista **Tipo de usuário**, também poderá clicar nas reticências **(...)** para abrir a caixa de diálogo **Selecionar Usuário ou Grupo**.  
  
     **Nome de logon**  
     Insira o logon do usuário. Como alternativa, clique nas reticências **(...)** para abrir a caixa de diálogo **Selecionar Logon**. **Nome de logon** estará disponível se você ou selecionar **Usuário do SQL com logon** ou **Usuário do Windows** na lista **Tipo de usuário** .  
  
     **Senha** e **Confirmar Senha**  
     Digite uma senha para usuários que autenticam no banco de dados.  
  
     **Idioma padrão**  
     Insira o idioma padrão do usuário.  
  
     **Esquema padrão**  
     Insira o esquema que terá a propriedade dos objetos criados por esse usuário. Como alternativa, clique nas reticências **(...)** para abrir a caixa de diálogo **Selecionar Esquema**. **Esquema padrão** estará disponível se você ou selecionar **Usuário do SQL com logon**, **Usuário do SQL sem logon**ou **Usuário do Windows** na lista **Tipo de usuário** .  
  
     **Nome de certificado**  
     Insira o certificado a ser usado para o usuário de banco de dados. Opcionalmente, clique nas reticências **(...)** para abrir a caixa de diálogo **Selecionar Certificado**. **Nome de certificado** estará disponível se você selecionar **Usuário mapeado para um certificado** na lista **Tipo de Usuário** .  
  
     **Nome da chave assimétrica**  
     Insira a chave a ser usada para o usuário de banco de dados. Como alternativa, clique nas reticências **(...)** para abrir a caixa de diálogo **Selecionar Chave Assimétrica**. **Nome da chave assimétrica** estará disponível se você selecionar **Usuário mapeado para uma chave assimétrica** na lista **Tipo de usuário** .  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>Opções adicionais  
 A caixa de diálogo **Usuário de banco de dados – Novo** também oferece opções em quatro páginas adicionais: **Esquemas Proprietários**, **Associação**, **Protegíveis** e **Propriedades Estendidas**.  
  
-   A página **Esquemas Proprietários** lista todos os possíveis esquemas que podem ser possuídos pelo novo usuário de banco de dados. Para adicionar esquemas a ou removê-los de um usuário de banco de dados, sob **Esquemas possuídos por este usuário**, marque ou desmarque as caixas de seleção ao lado dos esquemas.  
  
-   A página **Associação** lista todas as funções de associação de banco de dados possíveis que podem pertencer ao novo usuário de banco de dados. Para adicionar funções a ou removê-los de um usuário de banco de dados, em **Associação à função de banco de dados**, marque ou desmarque as caixas de seleção ao lado das funções.  
  
-   A página **Protegíveis** lista todos os protegíveis e as permissões possíveis nesses protegíveis que podem ser concedidos ao logon.  
  
-   A página **Propriedades estendidas** permite adicionar propriedades personalizadas a usuários de banco de dados. As opções a seguir estão disponíveis nesta página.  
  
     **Banco de Dados**  
     Exibe o nome do banco de dados selecionado. Esse campo é somente leitura.  
  
     **Ordenação**  
     Exibe a ordenação usada para o banco de dados selecionado. Esse campo é somente leitura.  
  
     **Propriedades**  
     Exiba ou especifique as propriedades estendidas do objeto. Cada propriedade estendida consiste em um par de nomes/valores de metadados associado ao objeto.  
  
     **Reticências (...)**  
     Clique nas reticências **(...)** depois do **Valor** para abrir a caixa de diálogo **Valor da Propriedade Estendida**. Digite ou exiba o valor da propriedade estendida neste local maior. Para obter mais informações, consulte [Caixa de diálogo Valor da Propriedade Estendida](../../databases/value-for-extended-property-dialog-box.md).  
  
     **Delete (excluir)**  
     Remove a propriedade estendida selecionada.  
  
##  <a name="TsqlProcedure"></a> Criar um usuário usando o T-SQL  
    
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra **Padrão** , clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Creates the login AbolrousHazem with password '340$Uuxwp7Mcxo7Khy'.  
    CREATE LOGIN AbolrousHazem   
        WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
    GO  
  
    -- Creates a database user for the login created above.  
    CREATE USER AbolrousHazem FOR LOGIN AbolrousHazem;  
    GO  
    ```  
  
 Para obter mais informações, veja [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md), que contém muitos outros exemplos do [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Criar um logon](../../../relational-databases/security/authentication-access/create-a-login.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/create-login-transact-sql.md)  
  
  
