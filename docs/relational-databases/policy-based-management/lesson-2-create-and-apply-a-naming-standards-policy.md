---
title: 'Lição 2: Criar e aplicar uma política de padrões de nomenclatura | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: security
ms.prod_service: database-engine
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 87e51f4e-156c-4def-8572-76a15075d75e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: be32b0412b71f4f6e6ca2044bfdd6ead682572c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087170"
---
# <a name="lesson-2-create-and-apply-a-naming-standards-policy"></a>Lição 2: Criar e aplicar uma política de nomeação de padrões
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Alguns tipos de políticas de Gerenciamento Baseado em Políticas podem criar gatilhos para aplicar conformidade futura com a política. Nesta lição, você cria uma política que aplica uma nomeação padrão para tabelas. Então, você testa a política tentando criar uma tabela que viola a política.  


## <a name="prerequisites"></a>Prerequisites
Para concluir este tutorial, é necessário ter o SQL Server Management Studio e acesso a um servidor que está executando o SQL Server.

- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instalar o [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
  
## <a name="create-the-finance-database"></a>Criar o banco de dados Finance  
  
1.  Em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma janela de consulta e execute a instrução a seguir:  
  
    ```sql  
    CREATE DATABASE Finance ;  
    GO  
    ```  
  
2.  No Pesquisador de Objetos, clique em **Bancos de Dados**e, em seguida, pressione F5 para atualizar a lista de bancos de dados.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="create-the-finance-tables-condition"></a>Criar a condição de tabelas Finance 

1.  No Pesquisador de Objetos, expanda **Gerenciamento**, **Gerenciamento de Política**, clique com o botão direito do mouse em **Condições**e clique em **Nova Condição**. 

   ![Nova condição](Media/lesson-2-create-and-apply-a-naming-standards-policy/new-condition.png)
  
2.  Na caixa de diálogo **Criar Nova Condição** , na caixa **Nome** , digite **Tabelas de Finanças**.  
    1. Na lista **Faceta** , selecione **Nome com Diversas Partes**. 
    1. Na área **Expressão**, na caixa **Campo**, selecione **@Name** ; na caixa **Operador**, selecione **Like**; e na caixa **Valor**, digite ```'fintbl%'``` para forçar todos os nomes de tabelas a começar com as letras **fintbl**.
    1. Na página **Descrição** , digite **Os nomes da tabela de Finanças deve começar com fintbl**e, em seguida, clique em **OK** para criar a condição.  

    ![Condição de tabelas Finance](Media/lesson-2-create-and-apply-a-naming-standards-policy/finance-tables-condition.png)
 
## <a name="create-the-finance-name-policy"></a>Criar a política de nome de Finance  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em **Políticas**e clique em **Nova Política**.  

   ![Nova política](Media/lesson-2-create-and-apply-a-naming-standards-policy/new-policy.png)
  
2.  Na caixa de diálogo **Criar Nova Política** , na caixa **Nome** , digite **Nome de Finanças**.
    1. Na lista **Verificar condição** , selecione **Tabelas de Finanças**. Isso está na área **Nome com Diversas Partes** . 
    1. Na área **Contra** você verá uma lista dos objetos de banco de dados que poderiam aplicar essa política. Selecione a caixa de seleção para **Cada Tabela**.
    1. Selecione a lista **Habilitado** . (A caixa **Habilitado** não se aplica a políticas **Sob Demanda** .)
    1. Na lista **Modo de Avaliação** , selecione **Ao alterar: impedir**. Isso aplicará a política criando um gatilho de banco de dados no banco de dados Finanças. 
    1. Na lista **Restrição de servidor** , selecione **Nenhum**. 
    1. Na página **Descrição**, adicione a descrição "Nomes de tabela no banco de dados Finance devem conter 'fintbl%'." 
    1. Volte à página **Geral** e, na área **Cada Banco de Dados**, expanda **Tudo** e clique em **Nova condição**.

    ![Create nova política de nome de Finance](Media/lesson-2-create-and-apply-a-naming-standards-policy/create-new-policy-finance-name.png)
  
6.  Na caixa de diálogo **Criar Nova Condição** , na caixa **Nome** , digite **Banco de Dados de Finanças**.
    1. Na caixa **Expressão**, complete a expressão para incluir @Name = 'Finance' e clique em **OK** para fechar a página de condição. 
  
    ![Criar nova condição "finance database"](Media/lesson-2-create-and-apply-a-naming-standards-policy/create-new-condition.png)

    > [!NOTE]  
    > Você poderia ter a guia fora da caixa **Valor** para habilitar o botão **OK** .  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="create-the-finance-policy-category"></a>Criar a categoria da política de Finance  
  
1.  Em Pesquisador de Objetos, expanda **Gerenciamento**, clique com o botão direito do mouse em **Gerenciamento de Política**e clique em **Gerenciar Categorias**.  

   ![Gerenciar categorias](Media/lesson-2-create-and-apply-a-naming-standards-policy/manage-categories.png)
  
2.  Na caixa de diálogo **Gerenciar Categorias de Política** , em **Nome**, digite **Finanças** na caixa em branco e desmarque **Autorizar Assinaturas de Banco de Dados**. A opção**Autorizar Assinaturas de Banco de Dados** forçará todos os bancos de dados na instância a assinarem as políticas que pertencem a esta categoria de política. Para esta lição, somente o banco de dados Finanças deve assinar a política Nome Financeiro.  

    ![Gerenciar categorias de política](Media/lesson-2-create-and-apply-a-naming-standards-policy/manage-policy-categories.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="subscribe-to-the-finance-policy-category"></a>Assinar a categoria de políticas de Finance  
  
1.  Em Pesquisador de Objetos, expanda **Bancos de Dados**, clique com o botão direito do mouse em **Finanças**, aponte para **Políticas**e clique em **Categorias**. 

   ![Categorias de política de Finance](Media/lesson-2-create-and-apply-a-naming-standards-policy/finance-categories.png)
  
2.  Selecione a caixa de seleção **Assinado** da categoria **Finanças** .  

   ![Assinar a política de finanças](Media/lesson-2-create-and-apply-a-naming-standards-policy/subscribe-to-finance.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="test-the-enforcement-of-the-finance-name-policy"></a>Testar a imposição da política de nome de Finance  
  
1.  Em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma janela de consulta. Execute as instruções a seguir que tentam criar uma tabela que viola a política **Nome de Finanças** . A tabela viola a política porque o nome de tabela não começa com as letras **fintbl**.  
  
    ```sql  
    USE Finance ;  
    GO  
    CREATE TABLE NewTable  
    (Col1 int) ;  
    GO    
    ```  
  
    Observe que a política impede que a tabela seja criada e retorne uma mensagem informativa que forneça o nome da política. 

   ```
     Policy 'Finance Name' has been violated by 'SQLSERVER:\SQL\SQL\SQL2017\Databases\Finance\Tables\dbo.NewTable'.
     This transaction will be rolled back.
     Policy condition: '@Name LIKE 'fintbl%''
     Policy description: 'Tables names in the Finance database must contain 'fintbl%''.
     Additional help: '' : ''
     Statement: 'CREATE TABLE NewTable  
         (Col1 int)'.
     Msg 515, Level 16, State 2, Procedure msdb.sys.sp_syspolicy_execute_policy, Line 69 [Batch Start Line 2]
     Cannot insert the value NULL into column 'target_query_expression', table 'msdb.dbo.syspolicy_policy_execution_history_details_internal'; column does not allow nulls. INSERT fails.
     The statement has been terminated.
   ``` 
  
2.  Para fornecer um nome válido, modifique o código como se segue e execute a instrução novamente.  
  
    ```sql  
    USE Finance ;  
    GO  
    CREATE TABLE fintblNewTable  
    (Col1 int) ;  
    GO    
    ```  
  
    Neste momento, a tabela é criada.  
  
## <a name="apply-the-policy-to-the-whole-server"></a>Aplicar a política ao servidor inteiro  
  
1.  Atualmente, o banco de dados Finanças se inscreve na categoria de política Finanças. Em muitos casos, é mais fácil aplicar a categoria de política ao servidor inteiro. Em Pesquisador de Objetos, expanda **Gerenciamento**, clique com o botão direito do mouse em **Gerenciamento de Política**e clique em **Gerenciar Categorias**.  
  
2.  Na caixa de diálogo **Gerenciar Categorias de Política** , localize a categoria Finanças e marque a caixa de seleção **Autorizar Assinaturas de Bancos de Dados** para a categoria Finanças.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] Agora a categoria Finanças se aplica a todos os bancos de dados, mas a condição que você criou restringe a política Nome de Finanças ao banco de dados Finanças. Isso mostra como você pode usar combinações complexas de políticas de destino de forma a aplicá-las corretamente em muitos servidores.  
  
## <a name="summary"></a>Resumo  
Este tutorial mostrou como criar condições do Gerenciamento Baseado em Políticas, políticas e grupos de políticas e como aplicar filtros e verificar a compatibilidade de destinos de Gerenciamento Baseado em Políticas.  
  
## <a name="next"></a>Próximo  
Este tutorial está concluído. Para retornar ao início, visite o [Tutorial: Administração de servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/tutorial-administering-servers-by-using-policy-based-management.md).  
  
Para obter uma lista de tutoriais, consulte [Tutoriais do SQL Server 2016](../../sql-server/tutorials-for-sql-server-2016.md).  
  
## <a name="see-also"></a>Consulte Também  
[Administrar servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
