---
title: Atualizar um projeto de teste mais antigo contendo testes de unidade de banco de dados | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 42782ff3-e8cf-4c9d-8dac-a95b236edfc4
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bfe8116a8467a30fb90399b292847cf20e7010f7
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086868"
---
# <a name="upgrade-an-older-test-project-containing-database-unit-tests"></a>Atualizar um projeto de teste mais antigo contendo testes de unidade de banco de dados
Você pode atualizar um projeto de teste mais antigo, que foi criado no Visual Studio 2010 e que contém testes de unidade de banco de dados, para usar o novo tempo de execução e as ferramentas do teste de unidade de banco de dados do SQL Server Data Tools. Assim que você tiver atualizado um projeto mais antigo, você poderá adicionar os testes de unidade do SQL Server ao projeto (confira [Criar e definir testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md) para obter mais informações.  
  
> [!TIP]  
> Se você estiver usando o Visual Studio 2010, depois de adicionar os testes de unidade do SQL Server a um projeto de teste, não deverá adicionar testes de unidade usando o modelo de teste de unidade de banco de dados mais antigo. Se o fizer, precisará converter para o projeto novamente antes de os testes serem executados corretamente.  
  
Se você tiver um projeto de banco de dados de teste que foi criado em uma versão mais antiga que o Visual Studio 2010, poderá usar as informações em [Como atualizar testes de unidade de banco de dados de versões antigas do Visual Studio](http://msdn.microsoft.com/library/dd193412(VS.100).aspx) para atualizar seu projeto de banco de dados para o Visual Studio 2010, antes de atualizar o projeto para o SQL Server Data Tools.  
  
### <a name="initiating-an-upgrade"></a>Iniciando uma atualização  
  
-   Você pode iniciar uma atualização de projeto do menu de contexto para um projeto de teste.  
  
    Em alguns casos, o SQL Server Data Tools exibirá uma caixa de diálogo da qual você pode iniciar uma atualização de projeto de teste.  
  
-   Atualizar o projeto remove a referência de assembly para a estrutura de teste de banco de dados mais antiga e adiciona uma referência para a nova estrutura e um assembly de adaptador. O arquivo app.config também é atualizado.  
  
    > [!NOTE]  
    > Se seu projeto de teste tiver arquivos de código DatabaseSetup e SQLDatabaseSetup, atualizar o projeto para o SQL Server Data Tools excluirá o arquivo DatabaseSetup da compilação. Você pode remover o arquivo DatabaseSetup se ele for excluído da compilação.  
  
-   Depois da conversão, os testes de unidade de banco de dados existentes criados com o modelo mais antigo usarão tipos no assembly do adaptador para acessar a nova estrutura. O uso de um assembly de adaptador significa que o procedimento de atualização não modificou seus scripts de teste e código. Se você adicionar um teste de unidade do SQL Server ao projeto, o novo teste referenciará a nova estrutura diretamente e não por meio de um adaptador. Você pode escolher atualizar manualmente seu código existente para usar a nova estrutura para ficar consistente com novos testes, mas isso não é obrigatório.  
  
## <a name="see-also"></a>Consulte Também  
[Verificar o código do banco de dados usando os testes de unidade do SQL Server](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
