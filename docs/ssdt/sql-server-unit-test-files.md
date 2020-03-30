---
title: Arquivos de teste de unidade do SQL Server
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: cee093c9-b97d-4fb0-b80f-806d071259dc
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 45c43cbf392e795eb0f5aee6876ad9e649b09788
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75256331"
---
# <a name="sql-server-unit-test-files"></a>Arquivos de teste de unidade do SQL Server

Como os testes de unidade para o código gerenciado, os testes de unidade do SQL Server residem em projetos de teste. Você pode ver os itens que compõem um teste de unidade do SQL Server na hierarquia de um projeto de teste no **Gerenciador de Soluções**.  
  
Um teste de unidade do SQL Server consiste em vários itens contidos em vários arquivos. A tabela a seguir descreve os arquivos que interagem para formar um teste de unidade do SQL Server.  
  
|**Arquivo**|**Descrição**|  
|------------|-------------------|  
|.cs ou .vb|Esse arquivo de código-fonte contém uma classe decorada com o atributo [TestClass]. Essa classe contém um único método de teste para cada um dos testes de unidade do SQL Server independente. Esses métodos são decorados com o atributo [TestMethod].<br /><br />Cada método de teste contém o código apropriado para exercer o script de teste Transact\-SQL. Esse código é gerado quando os métodos de teste são criados, e você pode modificá-lo.<br /><br />**OBSERVAÇÃO:** se você clicar duas vezes nesse arquivo no **Gerenciador de Soluções**, a classe de teste será aberta no Designer de Teste de Unidade do SQL Server. Para abrir o arquivo .cs ou .vb para ver seu código-fonte, clique com o botão direito do mouse no arquivo no **Gerenciador de Soluções** e clique em **Exibir Código**.|  
|.resx|Este arquivo de recurso contém os scripts Transact\-SQL definidos para todos os testes no arquivo .cs ou .vb associado. Esse grupo de scripts inclui os scripts de pré-teste, de teste e de pós-teste. O arquivo de recurso contém XML, que você pode editar. O arquivo de recurso é compilado no assembly de teste.<br /><br />Você deve codificar os scripts Transact\-SQL usando o **Designer de Teste de Unidade do SQL Server**. Para saber mais sobre os scripts que são usados em testes de unidade do SQL Server, consulte [Scripts nos testes de unidade do SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md).|  
|app.config|Esse arquivo armazena as cadeias de conexão de banco de dados do projeto de teste, além de outras configurações de teste de unidade do SQL Server, como tempo limite do comando. Para saber mais, confira [Scripts nos testes de unidade do SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md).|  
|SQLDatabaseSetup.cs ou SQLDatabaseSetup.vb|Esse arquivo contém uma classe que prepara o ambiente de teste para todos os testes de unidade do SQL Server no projeto de teste. Com base nessas configurações no arquivo app.config, ele pode implantar um Projeto de Banco de Dados do SQL Server para o banco de dados de teste.|  
  
## <a name="see-also"></a>Consulte Também  
[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Verificar o código do banco de dados usando os testes de unidade do SQL Server](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
[Scripts nos testes de unidade do SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md)  
  
