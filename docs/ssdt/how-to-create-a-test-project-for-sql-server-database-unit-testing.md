---
title: Como criar um projeto de teste para testes de unidade de banco de dados do SQL Server| Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4b3e7ba8-b565-4689-af1a-34cc255b7c60
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9f641380e18dbcb042e36704627e1e39e2f9a4e7
ms.sourcegitcommit: b8e2e3e6e04368aac54100c403cc15fd4e4ec13a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45563643"
---
# <a name="how-to-create-a-test-project-for-sql-server-database-unit-testing"></a>Como: Criar um projeto de teste para testes de unidade de banco de dados do SQL Server
Antes de gravar testes de unidade que avaliem objetos de banco de dados, você deve primeiro criar um projeto de teste. O projeto contém testes de unidade do SQL Server, mas pode conter também outros tipos de teste.  
  
Você pode colocar todos os testes de unidade do SQL Server de um projeto de banco de dados em um único projeto de teste. No entanto, talvez seja necessário criar projetos de teste adicionais com base nas suas respostas às seguintes perguntas:  
  
|||  
|-|-|  
|**Pergunta.**|**Decisão**|  
|Os diferentes testes de unidade do SQL Server precisam acessar conexões de banco de dados diferentes para a execução ou a validação do teste?|Em caso afirmativo, você precisará de mais de um projeto de teste. Não é possível especificar mais de uma conexão de banco de dados para a execução do teste. No entanto, você pode especificar uma conexão de banco de dados diferente para a validação do teste.|  
|Você deseja implantar projetos de banco de dados diferentes para testes de unidade diferentes?|Em caso afirmativo, você precisará de mais de um projeto de teste. Um projeto de teste somente pode implantar um único projeto de banco de dados.|  
  
Para saber mais, confira [Como configurar a execução do teste de unidade do SQL Server](../ssdt/how-to-configure-sql-server-unit-test-execution.md). Como alternativa à criação de vários projetos de teste, você também pode fornecer sua própria implementação [DatabaseTestService](https://msdn.microsoft.com/library/microsoft.data.schema.unittesting.databasetestservice.aspx) Microsoft.Data.Schema.UnitTesting.DatabaseTestService.  
  
Existem três opções para adicionar um projeto de teste a uma solução que contém um projeto de banco de dados:  
  
-   Adicionar um projeto de teste à solução. O projeto de teste contém um teste de unidade padrão, que você pode excluir. Esse projeto não contém uma classe de teste de unidade do SQL Server, que você deve adicionar.  
  
-   Adicione um novo teste de unidade do SQL Server no menu **Test**. Quando você adicionar o teste de unidade, o SQL Server Data Tools também criará um projeto de teste se você solicitá-lo. Este projeto contém uma classe de teste de unidade do SQL Server. As classes de teste da unidade do SQL Server contêm um ou mais testes de unidade.  
  
-   Crie um teste de unidade a partir de um procedimento armazenado, função ou acionador de um projeto aberto no Pesquisador de Objetos do SQL Server. Quando você criar o teste de unidade, o SQL Server Data Tools também criará um projeto de teste se você solicitá-lo. Este projeto contém uma classe de teste de unidade do SQL Server. As classes de teste do SQL Server contêm um ou mais testes de unidade.  
  
Cada abordagem é descrita nos procedimentos a seguir.  
  
### <a name="to-add-a-test-project-to-an-existing-solution"></a>Para adicionar um projeto de teste a uma solução existente  
  
1.  No menu **Arquivo** , aponte para **Novo**e clique em **Projeto**.  
  
    A caixa de diálogo **Novo Projeto** será exibida.  
  
2.  Em **Modelos Instalados**, expanda o nó **SQL Server** e selecione **Projeto de Banco de Dados do SQL Server**.  
  
3.  Em **Nome**, digite um nome do projeto.  
  
### <a name="to-create-a-test-project-with-a-sql-server-unit-test-class"></a>Para criar um projeto de teste com uma classe de teste de unidade do SQL Server  
  
-   Siga o procedimento descrito em [Como criar um teste de unidade do SQL Server vazio](../ssdt/how-to-create-an-empty-sql-server-unit-test.md) ou [Como criar testes de unidade do SQL Server para funções, gatilhos e procedimentos armazenados ](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md).  
  
## <a name="see-also"></a>Consulte Também  
[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
  
