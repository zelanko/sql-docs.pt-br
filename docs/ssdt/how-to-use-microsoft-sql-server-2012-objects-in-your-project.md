---
title: 'Como fazer: usar objetos do Microsoft SQL Server 2012 no seu projeto | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 9baf122f-cf22-4860-98db-ef782cd972fc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 222b725e7e5497adaf679f710fa390dcea8aecf7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68034982"
---
# <a name="how-to-use-microsoft-sql-server-2012-objects-in-your-project"></a>Como fazer: Usar objetos do Microsoft SQL Server 2012 no seu projeto
Neste exemplo, você adicionará um objeto de sequência a um projeto de banco de dados destinado ao Microsoft SQL Server 2012.  
  
As sequências são introduzidas no Microsoft SQL Server 2012. Uma sequência é um objeto associado a um esquema definido pelo usuário que gera uma sequência de valores numéricos de acordo com a especificação com a qual a sequência foi criada. A sequência de valores numéricos é gerada em ordem crescente ou decrescente em um intervalo definido e pode seguir um ciclo (repetir-se) conforme solicitado.  Para saber mais sobre objetos de sequência, consulte [Números de sequência](htttp://msdn.microsoft.com/library/ff878058(SQL.110).aspx). Para saber mais sobre as novidades no Microsoft SQL Server 2012, confira [Novidades no SQL Server 2012](https://msdn.microsoft.com/library/bb500435(SQL.110).aspx).  
  
> [!WARNING]  
> Os procedimentos a seguir utilizam entidades criadas em procedimentos anteriores nas seções [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md) e [Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-add-a-new-sequence-object-to-your-project"></a>Para adicionar um novo objeto de sequência a seu projeto  
  
1.  Clique com o botão direito do mouse no projeto de banco de dados **TradeDev** no **Gerenciador de Soluções**, selecione **Adicionar** e **Novo Item**.  
  
2.  Clique em **Programabilidade** no painel esquerdo e selecione **Sequência**. Clique em **Adicionar** para adicionar o novo objeto ao projeto.  
  
3.  Substitua o código padrão pelo seguinte.  
  
    ```  
    CREATE SEQUENCE [dbo].[Seq1]  
    AS INT  
    START WITH 1  
    INCREMENT BY 1  
    MAXVALUE 1000  
    NO CYCLE  
    CACHE 10  
    ```  
  
4.  Se a plataforma de destino de seu projeto não estiver definida para o Microsoft SQL Server 2012, a **Lista de Erros** mostrará um erro de sintaxe para a instrução `CREATE SEQUENCE`. Para corrigir isso, siga o tópico [Como alterar a plataforma de destino e publicar um projeto de banco de dados](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md) para alterar a plataforma de destino de forma adequada.  
  
5.  Siga o tópico [Como alterar a plataforma de destino e publicar um projeto de banco de dados](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md) para publicar o projeto em um banco de dados em seu servidor conectado do Microsoft SQL Server 2012.  
  
### <a name="to-use-the-new-sequence-object"></a>Para usar o novo objeto de sequência  
  
1.  No Pesquisador de Objetos do SQL Server, clique com o botão direito do mouse no banco de dados em que publicou no procedimento anterior e selecione **Nova Consulta**.  
  
2.  Cole o código a seguir na janela de consulta.  
  
    ```  
    DECLARE @counter INT  
    SET @counter=0  
    WHILE @counter<10  
    BEGIN  
        SET @counter = @counter +1  
         INSERT dbo.Products (Id, Name, CustomerId) VALUES (NEXT VALUE FOR dbo.Seq1, 'ProductItem'+cast(@counter as varchar), 1)  
    END   
    GO  
    ```  
  
3.  Pressione o botão **Executar Consulta**.  
  
4.  No **Pesquisador de Objetos do SQL Server**, navegue até a tabela **Produtos** no banco de dados. Clique com o botão direito do mouse em **Exibir Dados** para examinar as linhas recém-adicionadas.  
  
