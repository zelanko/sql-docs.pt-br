---
title: Criar um usuário de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.DATABASEUSER.GENERAL.F1
- sql12.swb.user.securables.f1
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
manager: craigg
ms.openlocfilehash: 2fba39e592835f3c5e6dbffc6c8b6d384c5c837a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057306"
---
# <a name="create-a-database-user"></a>Criar um usuário de banco de dados
  Este tópico descreve como criar um usuário de banco de dados mapeado para um logon no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] por meio [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)]. O usuário de banco de dados é a identidade do logon quando é conectado a um banco de dados. O usuário de banco de dados pode usar o mesmo nome como o logon, mas isso não é requerido. Este tópico pressupõe que já exista um logon no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter informações sobre como criar um logon, consulte [criar um logon](create-a-login.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Plano de fundo](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar um usuário de banco de dados, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Plano de fundo  
 Um usuário é uma entidade de segurança no nível de banco de dados. Logons devem ser mapeados para um usuário de banco de dados para ser conectados a um banco de dados. Um logon pode ser mapeado para bancos de dados diferentes como usuários diferentes, mas pode ser mapeado somente como um usuário em cada banco de dados. Em um banco de dados parcialmente independente, um usuário pode ser criado sem logon. Para obter mais informações sobre os usuários de banco de dados independente, veja [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql). Se o usuário convidado em um banco de dados estiver habilitado, um logon que não estiver mapeado para um usuário de banco de dados poderá acessar o banco de dados como um usuário convidado.  
  
> [!IMPORTANT]  
>  O usuário convidado normalmente é desabilitado. Não habilite o usuário convidado, a menos que seja necessário.  
  
 Como uma entidade de segurança, permissões podem ser concedidas a usuários. O escopo de um usuário é o banco de dados. Para se conectar a um banco de dados específico na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], um logon deve ser mapeado para um usuário de banco de dados. Permissões, e não o logon, são concedidas dentro do banco de dados e são negadas ao usuário de banco de dados.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão `ALTER ANY USER` no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
##### <a name="to-create-a-database-user"></a>Para criar um usuário de banco de dados  
  
1.  No Pesquisador de Objetos, expanda a pasta **Bancos de Dados** .  
  
2.  Expanda o banco de dados no qual o novo usuário de banco de dados será criado.  
  
3.  Clique com o botão direito do mouse na pasta **Segurança** , aponte para **Novo**e selecione **Usuário...**.  
  
4.  Na caixa de diálogo **Usuário de banco de dados – Novo** da página **Geral** , selecione um dos seguintes tipos de usuário na lista **Tipo de usuário** : **Usuário do SQL com logon**, **Usuário do SQL sem logon**, **Usuário mapeado para um certificado**, **Usuário mapeado para uma chave assimétrica**ou **Usuário do Windows**.  
  
5.  Na caixa **Nome do usuário** , digite um nome para o novo usuário. Se você escolheu **Usuário do Windows** na lista **Tipo de usuário** , também poderá clicar nas reticências **(...)** para abrir a caixa de diálogo **Selecionar Usuário ou Grupo** .  
  
6.  Na caixa **Nome de logon** , digite o logon do usuário. Como alternativa, clique nas reticências **(…)** para abrir a caixa de diálogo **Selecionar Logon** . **Nome de logon** estará disponível se você ou selecionar **Usuário do SQL com logon** ou **Usuário do Windows** na lista **Tipo de usuário** .  
  
7.  Na caixa **Esquema padrão** , especifica o esquema que terá a propriedade dos objetos criados por esse usuário. Como alternativa, clique nas reticências **(…)** para abrir a caixa de diálogo **Selecionar Esquema** . **Esquema padrão** estará disponível se você ou selecionar **Usuário do SQL com logon**, **Usuário do SQL sem logon**ou **Usuário do Windows** na lista **Tipo de usuário** .  
  
8.  Na caixa **Nome do certificado** , digite o certificado a ser usado para o usuário de banco de dados. Opcionalmente, clique nas reticências **(…)** para abrir a caixa de diálogo **Selecionar Certificado** . **Nome de certificado** estará disponível se você selecionar **Usuário mapeado para um certificado** na lista **Tipo de Usuário** .  
  
9. Na caixa **Nome da chave assimétrica**  , digite a chave a ser usada para o usuário de banco de dados. Como alternativa, clique nas reticências **(…)** para abrir a caixa de diálogo **Selecionar Chave Assimétrica** . **Nome da chave assimétrica** estará disponível se você selecionar **Usuário mapeado para uma chave assimétrica** na lista **Tipo de usuário** .  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>Opções adicionais  
 A caixa de diálogo **Usuário do Banco de Dados – Novo** também oferece opções em quatro páginas adicionais: **Esquemas Proprietários**, **Associação**, **Protegíveis**e **Propriedades Estendidas**.  
  
-   A página **Esquemas Proprietários** lista todos os possíveis esquemas que podem ser possuídos pelo novo usuário de banco de dados. Para adicionar esquemas a ou removê-los de um usuário de banco de dados, sob **Esquemas possuídos por este usuário**, marque ou desmarque as caixas de seleção ao lado dos esquemas.  
  
-   A página **Associação** lista todas as funções de associação de banco de dados possíveis que podem pertencer ao novo usuário de banco de dados. Para adicionar funções a ou removê-los de um usuário de banco de dados, em **Associação à função de banco de dados**, marque ou desmarque as caixas de seleção ao lado das funções.  
  
-   A página **Protegíveis** lista todos os protegíveis e as permissões possíveis nesses protegíveis que podem ser concedidos ao logon.  
  
-   A página **Propriedades estendidas** permite adicionar propriedades personalizadas a usuários de banco de dados. As opções a seguir estão disponíveis nesta página.  
  
     **Banco de Dados**  
     Exibe o nome do banco de dados selecionado. Esse campo é somente leitura.  
  
     **Agrupamento**  
     Exibe o agrupamento usado para o banco de dados selecionado. Esse campo é somente leitura.  
  
     **Propriedades**  
     Exiba ou especifique as propriedades estendidas do objeto. Cada propriedade estendida consiste em um par de nomes/valores de metadados associado ao objeto.  
  
     **Reticências (...)**  
     Clique no botão de reticências **(…)** depois do **Valor** para abrir a caixa de diálogo **Valor da Propriedade Estendida** . Digite ou exiba o valor da propriedade estendida neste local maior. Para obter mais informações, consulte [Caixa de diálogo Valor da Propriedade Estendida](../../databases/value-for-extended-property-dialog-box.md).  
  
     **Delete (excluir)**  
     Remove a propriedade estendida selecionada.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-database-user"></a>Para criar um usuário de banco de dados  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
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
  
 Para obter mais informações, consulte [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql).  
  
## <a name="see-also"></a>Consulte também  
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](principals-database-engine.md)  
  
  
