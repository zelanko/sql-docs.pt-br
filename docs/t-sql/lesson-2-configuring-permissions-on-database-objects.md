---
title: 'Tutorial: Configurar permissões em objetos de BD'
ms.custom: seo-lt-2019
ms.date: 07/31/2018
ms.prod: sql
ms.technology: t-sql
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- database permissions
ms.assetid: f964b66a-ec32-44c2-a185-6a0f173bfa22
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 991bdef702b1ed298bb492172ef65c6d25d5d0ab
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75244752"
---
# <a name="lesson-2-configure-permissions-on-database-objects"></a>Lição 2: Configurar permissões em objetos de banco de dados
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
Conceder um acesso de usuário a um banco de dados envolve três etapas. Primeiro, crie um logon. O logon permite que o usuário se conecte ao [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]. Em seguida, configure o logon como um usuário no banco de dados especificado. E, finalmente, conceda essa permissão de usuário a objetos de banco de dados. Esta lição mostra essas três etapas e demonstra como criar uma exibição e um procedimento armazenado como o objeto.  

  >[!NOTE]
  > Esta lição baseia-se em objetos criados na [Lição 1 – Criar objetos de banco de dados](lesson-1-creating-database-objects.md). Conclua a Lição 1 antes de passar para a Lição 2. 

## <a name="prerequisites"></a>Prerequisites
Para concluir este tutorial, você precisa de acesso ao SQL Server Management Studio e a uma instância do SQL Server. 

- Instale o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

Se você não tiver acesso a uma instância do SQL Server, selecione sua plataforma nos links a seguir. Se você escolher Autenticação do SQL, use suas credenciais de logon do SQL Server.
- **Windows**: [Baixe o SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- **macOS**: [baixe o SQL Server 2017 no Docker](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker).

[!INCLUDE[Freshness](../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="create-a-login"></a>Criar um logon
Para acessar o [!INCLUDE[ssDE](../includes/ssde-md.md)], os usuários precisam de um logon. O logon pode representar a identidade do usuário como conta do Windows ou como membro de um grupo do Windows, ou o logon pode ser um logon do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que exista apenas no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Sempre que possível, você deverá usar a Autenticação do Windows.  
  
Por padrão, os administradores têm acesso completo ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]no seu computador. Nesta lição, pretendemos ter um usuário menos privilegiado. Dessa forma, você criará uma nova conta local de Autenticação do Windows em seu computador. Para fazer isso, você precisa ser administrador do computador. E conceder acesso ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]ao novo usuário.  
  
### <a name="create-a-new-windows-account"></a>Criar uma nova conta do Windows  
  
1.  Clique em **Iniciar**, em **Executar**, na caixa **Abrir** , digite **%SystemRoot%\system32\compmgmt.msc /s**e clique em **OK** para abrir o programa de Gerenciamento do Computador. 
2.  Em **Ferramentas do Sistema**, expanda **Usuários e Grupos Locais**, clique com o botão direito do mouse em **Usuários**e clique em **Novo Usuário**.    
3.  Na caixa **Nome de usuário** digite **Mary**.    
4.  Na caixa **Senha** e **Confirmar senha** , digite uma senha forte e clique em **Criar** para gerar um novo usuário local do Windows.  
  
### <a name="create-a-sql-login"></a>Criar um logon do SQL  

Em uma janela do Editor de Consulta do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], digite e execute o código a seguir substituindo `computer_name` pelo nome de seu computador. `FROM WINDOWS` indica que o Windows autenticará o usuário. O argumento opcional `DEFAULT_DATABASE` é conectado `Mary` ao banco de dados `TestData` , a menos que a cadeia de caracteres de conexão indique outro banco de dados. Essa instrução introduz o ponto-e-vírgula como término opcional para uma instrução [!INCLUDE[tsql](../includes/tsql-md.md)] .
  
  ```sql  
  CREATE LOGIN [computer_name\Mary]  
      FROM WINDOWS  
      WITH DEFAULT_DATABASE = [TestData];  
  GO  
  ```  
  
  Isso autoriza o nome de usuário `Mary`, autenticado pelo seu computador, a acessar a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se houver mais de uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no computador, você deverá criar o logon em cada instância que `Mary` deve acessar.    
  > [!NOTE]  
  > Como `Mary` não é uma conta de domínio, esse nome de usuário só poderá ser autenticado nesse computador. 


## <a name="grant-access-to-a-database"></a>Conceder acesso a um banco de dados
Mary agora tem acesso a esta instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], mas não tem permissão para acessar os bancos de dados. Ela não tem acesso nem mesmo ao seu banco de dados padrão **TestData** até que você a autorize como usuária de um banco de dados.  
  
Para conceder acesso à Mary, alterne para o banco de dados **TestData** e, em seguida, use a instrução CREATE USER para mapear o logon dela para um usuário nomeado Mary.  
  
### <a name="to-create-a-user-in-a-database"></a>Para criar um usuário em um banco de dados  
  
Digite e execute as instruções a seguir (substituindo `computer_name` pelo nome de seu computador) para conceder acesso à `Mary` ao banco de dados `TestData` .
  
 ```sql  
 USE [TestData];  
 GO  
 
 CREATE USER [Mary] FOR LOGIN [computer_name\Mary];  
 GO    
 ```  
  
 Agora, Mary tem acesso ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e ao banco de dados `TestData` .  


## <a name="create-views-and-stored-procedures"></a>Criar exibições e procedimentos armazenados
Como administrador, você pode executar SELECT na tabela **Produtos** e na exibição **vw_Names** , além de executar o procedimento **pr_Names** ; no entanto, Marina não pode. Para conceder as permissões necessárias à Mary, use a instrução GRANT.  

### <a name="grant-permission-to-stored-procedure"></a>Conceder permissão ao procedimento armazenado  
Execute a instrução a seguir para conceder a `Mary` a permissão `EXECUTE` para o procedimento armazenado `pr_Names` .
  
  ```sql  
  GRANT EXECUTE ON pr_Names TO Mary;  
  GO  
  ```  
  
Nesse cenário, Mary pode acessar apenas a tabela **Products** usando o procedimento armazenado. Para que Mary possa executar a instrução SELECT na exibição, você também deve executar `GRANT SELECT ON vw_Names TO Mary`. Para remover acesso a objetos de banco de dados, use a instrução REVOKE.  
  
> [!NOTE]  
> Se a tabela, a exibição e o procedimento armazenado não pertencerem ao mesmo esquema, a concessão de permissões ficará mais complexa.  
  
### <a name="about-grant"></a>Sobre GRANT  
É preciso ter permissão EXECUTE para executar um procedimento armazenado. É preciso ter permissões SELECT, INSERT, UPDATE e DELETE para acessar e alterar dados. A instrução GRANT também é usada para outras permissões, como permissão para criar tabelas.  
  
## <a name="next-steps"></a>Próximas etapas
O próximo artigo ensina a remover objetos de banco de dados criados nas outras lições. 

Vá até o próximo artigo para saber mais:
> [!div class="nextstepaction"]
>[Próximas etapas](lesson-3-deleting-database-objects.md)
  
