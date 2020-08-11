---
title: Criando e definindo testes de unidade do SQL Server
description: Saiba mais sobre os testes de unidade do SQL Server. Veja fontes de informações sobre como criar e executar testes de unidade, solucionar problemas e executar outras tarefas relacionadas.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 3c082177-a2b1-4fde-8833-b49b2a351815
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 861014b336d9f75c2df1dfc7888a28eb663575de
ms.sourcegitcommit: b860fe41b873977649dca8c1fd5619f294c37a58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2020
ms.locfileid: "85518746"
---
# <a name="creating-and-defining-sql-server-unit-tests"></a>Criando e definindo testes de unidade do SQL Server

Você pode executar testes de unidade do SQL Server para verificar se as alterações feitas em um ou mais objetos de banco de dados de um esquema interromperam a funcionalidade existente em um aplicativo de banco de dados. Esses testes complementam os testes de unidade criados pelos desenvolvedores de software. Você deve executar os dois tipos de teste para verificar o comportamento do aplicativo.  
  
Você pode verificar o comportamento de qualquer objeto do esquema adicionando um teste de unidade do SQL Server e adicionando um script Transact\-SQL para testar esse objeto. Como alternativa, você pode gerar automaticamente um stub de um script Transact\-SQL caso queira verificar o comportamento de uma função, um gatilho ou um procedimento armazenado. Após gerar o stub, personalize-o para obter resultados significativos.  
  
> [!NOTE]  
> Você pode criar um teste vazio, adicionar código a ele e executá-lo sem estar com um projeto de banco de dados do SQL Server aberto. No entanto, você não pode gerar automaticamente um stub Transact\-SQL que teste uma função, um gatilho ou um procedimento armazenado sem abrir o projeto que contém o objeto a ser testado.  
  
## <a name="common-tasks"></a>Tarefas comuns  
Na tabela a seguir, é possível localizar descrições de tarefas comuns que oferecem suporte a esse cenário e links para mais informações sobre como concluir essas tarefas com êxito.  
  
|Tarefas comuns|Conteúdo de suporte|  
|----------------|----------------------|  
|**Adquira prática de trabalho**: você pode seguir um passo a passo introdutório para familiarizar-se com as etapas de criação e execução de um teste de unidade simples do SQL Server.|-   [Passo a passo: Criar e executar um teste de unidade do SQL Server](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)|  
|**Saiba mais sobre os testes de unidade do SQL Server**: você pode aprender mais sobre os arquivos e os scripts que compõem um teste de unidade do SQL Server. Além disso, é possível obter mais informações sobre como usar as condições de teste e asserções Transact\-SQL nos testes de unidade.|-   [Scripts nos testes de unidade do SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md)<br />-   [Arquivos de teste de unidade do SQL Server](../ssdt/sql-server-unit-test-files.md)<br />-   [Usar condições de teste nos testes de unidade do SQL Server](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)<br />-   [Usar asserções Transact-SQL nos testes de unidade do SQL Server](../ssdt/using-transact-sql-assertions-in-sql-server-unit-tests.md)|  
|**Criar um ou mais projetos de teste**: você deve criar testes de unidade do SQL Server em um projeto de teste. Se você criar um teste de unidade do SQL Server usando o Pesquisador de Objetos do SQL Server antes de criar um projeto de teste, o projeto será criado para você. Você poderá criar mais de um projeto de teste se, por exemplo, quiser usar planos de geração de dados ou configurações de implantação diferentes em conjuntos de teste diferentes. Ao criar o projeto de teste, você poderá definir configurações de teste (como a cadeia de conexão), configurações de implantação e um plano de geração de dados a ser usado nesse projeto.|-   [Como Criar um projeto de teste para testes de unidade de banco de dados do SQL Server](../ssdt/how-to-create-a-test-project-for-sql-server-database-unit-testing.md)<br />-|  
|**Configure como o teste de unidade é executado**: você pode especificar a cadeia de conexão para o banco de dados no qual executará os testes, o plano de geração de dados e as configurações de implantação. Você define essas configurações quando adiciona pela primeira vez um teste de unidade do SQL Server ao projeto, mas também pode modificá-las posteriormente.|-   [Como configurar a execução do teste de unidade do SQL Server](../ssdt/how-to-configure-sql-server-unit-test-execution.md)<br />-   [Visão geral das cadeias de conexão e permissões](../ssdt/overview-of-connection-strings-and-permissions.md)|  
|**Crie um teste de unidade do SQL Server**: você pode criar stubs de código Transact\-SQL para testes de unidade do SQL Server que verificam o comportamento de uma função, um gatilho ou um procedimento armazenado. Também é possível criar um teste de unidade do SQL Server vazio e, em seguida, adicionar o código Transact\-SQL para testar outros tipos de objetos de banco de dados.|-   [Como Criar testes de unidade do SQL Server para funções, gatilhos e procedimentos armazenados](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)<br />-   [Como Criar um teste de unidade do SQL Server vazio](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)|  
|**Escreva o código para um teste de unidade do SQL Server**: após criar um teste de unidade, modifique ou escreva o código Transact\-SQL para testar um objeto de banco de dados. Para cada teste, defina uma ou mais condições de teste que determinam se o teste será aprovado ou reprovado. Para testes mais complexos, você pode modificar o código Visual Basic ou Visual C\# no projeto de banco de dados. Por exemplo, você pode escrever um teste de unidade que seja executado no escopo de uma única transação.|-   [Como Abrir um teste de unidade do SQL Server a ser editado](../ssdt/how-to-open-a-sql-server-unit-test-to-edit.md)<br />-   [Como Adicionar condições de teste a testes de unidade do SQL Server](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md)<br />-   [Como Gravar um teste de unidade do SQL Server executado no escopo de uma única transação](../ssdt/how-to-write-sql-server-unit-test-that-runs-in-single-transaction-scope.md)<br />-   [Atalhos de teclado do designer de teste de unidade do SQL Server](../ssdt/keyboard-shortcuts-for-sql-server-unit-test-designer.md)|  
|**Solucionar problemas**: você pode obter mais informações sobre como solucionar problemas comuns no SQL Server.|-   [Solucionar problemas de teste de unidade do banco de dados SQL Server](../ssdt/troubleshooting-sql-server-database-unit-testing-issues.md)|  
  
## <a name="related-scenarios"></a>Cenários relacionados  
[Executar testes de unidade do SQL Server](../ssdt/running-sql-server-unit-tests.md)  
Depois que você criar os testes de unidade do SQL Server, poderá executá-los na janela Modo de Teste, no Designer de Teste de Unidade do SQL Server ou usando o Team Foundation Build.  
  
[Cenário: definir condições de teste personalizadas para testes de unidade de banco de dados](https://msdn.microsoft.com/library/dd193282(VS.100).aspx)  
Você pode criar uma condição de teste personalizada para testar um comportamento que as condições de teste padrão não podem verificar.  
  
## <a name="see-also"></a>Consulte Também  
[Verificar o código do banco de dados usando os testes de unidade do SQL Server](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
