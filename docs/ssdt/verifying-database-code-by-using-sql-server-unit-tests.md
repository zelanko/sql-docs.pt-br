---
title: Verificar o código do banco de dados usando os testes de unidade do SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 003713e2-de6b-4277-a0a8-7d1f2f4ffb39
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 597cebf9db40c2e119949c86341b4817a51c38ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65102004"
---
# <a name="verifying-database-code-by-using-sql-server-unit-tests"></a>Verificando o código do banco de dados usando os testes de unidade do SQL Server
Você pode usar os testes de unidade do SQL Server para estabelecer um estado de linha de base para o banco de dados e verificar todas as alterações subsequentes feitas nos objetos de banco de dados.  
  
Para estabelecer um estado de linha de base para um banco de dados, você cria um projeto de teste e escreve conjuntos de Transact\-SQL que operam em seus objetos de banco de dados. Ao usar esses testes, você pode verificar em um ambiente de desenvolvimento isolado se esses objetos funcionam conforme o esperado. O teste de unidade do SQL Server funciona bem em combinação com o desenvolvimento do banco de dados offline usando projetos de banco de dados do SQL Server (confira [Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md) para obter mais informações). Assim que você tiver a linha de base definida dos testes de unidade do SQL Server, poderá usar esses testes para verificar se o banco de dados está funcionando corretamente antes de fazer check-in das alterações para o controle de versão.  
  
Você pode criar testes que verifiquem as alterações feitas em qualquer objeto de banco de dados. Além de isso, você pode gerar automaticamente stubs de código Transact\-SQL que testem funções, gatilhos e procedimentos armazenados de banco de dados.  
  
> [!NOTE]  
> Você pode criar e executar testes de unidade do SQL Server sem ter um projeto de banco de dados aberto. No entanto, se você quiser gerar scripts de teste automaticamente para testar objetos de banco de dados específicos do projeto, abra o projeto de banco de dados que contém os objetos a serem testados.  
  
À medida que você ou os membros da equipe alterarem o esquema de banco de dados, você poderá usar esses testes para verificar se as alterações prejudicaram a funcionalidade existente. Crie testes de unidade do SQL Server para complementar os testes de unidade de software criados pelos desenvolvedores de software. Você deve concluir os dois conjuntos de teste para verificar o comportamento geral do aplicativo.  
  
Os testes de unidade podem verificar se os procedimentos terão êxito ou apresentarão falha nos momentos esperados. Os testes que verificam se as falhas apropriadas ocorrem são denominados testes negativos.  
  
## <a name="visual-studio-editions-support-for-sql-server-unit-tests"></a>Suporte das Edições do Visual Studio para testes de unidade do SQL Server  
O recurso de testes de unidade do SQL Server, que foi adicionado na atualização de dezembro de 2012 do SQL Server Data Tools, permite criar, modificar e executar testes de unidade do SQL Server no Visual Studio 2010 Professional e no Visual Studio 2012 Professional e em edições superiores.  
  
Para garantir a instalação da atualização mais recente do SQL Server Data Tools, acesse a [Caixa de diálogo Verificar Atualizações](../ssdt/check-for-updates-dialog-box.md).  
  
O shell do SQL Server Data Tools integrado do Visual Studio 2010 e do Visual Studio 2012 não oferece suporte a testes de unidade do SQL Server.  
  
## <a name="common-tasks"></a>Tarefas comuns  
Na tabela a seguir, é possível localizar descrições de tarefas comuns que oferecem suporte a esse cenário e links para mais informações sobre como concluir essas tarefas com êxito.  
  
|Tarefas comuns|Conteúdo de suporte|  
|----------------|----------------------|  
|**Obtenha treinamento prático:** você pode seguir um passo a passo introdutório para familiarizar-se com as etapas de criação e execução de um teste de unidade simples do SQL Server. Este passo a passo inclui um exemplo de um teste de unidade negativo do SQL Server.|[Passo a passo: Criar e executar um teste de unidade do SQL Server](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)|  
|**Definir testes de unidade do SQL Server:** você deve criar testes de unidade do SQL Server nos respectivos projetos. Defina as configurações desse projeto e defina uma ou mais condições de teste para cada teste.|[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)<br /><br />[Usar condições de teste nos testes de unidade do SQL Server](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)|  
|**Executar testes de unidade do SQL Server:** após definir um ou mais testes de unidade, você os executa, depura os problemas e examina os resultados de teste.|[Executar testes de unidade do SQL Server](../ssdt/running-sql-server-unit-tests.md)|  
|**Gerenciar grupos de testes (Visual Studio 2010):** você poderá organizar testes em grupos caso eles normalmente sejam executados ao mesmo tempo. Ainda há suporte para as listas de teste, mas para os novos grupos de teste, você deve considerar as categorias de teste. Por exemplo, você pode criar uma categoria de teste para os testes dos gatilhos ou de todos os objetos em um *esquema específico*.|[Definir categorias de teste para agrupar os testes](https://msdn.microsoft.com/library/dd286595(VS.100).aspx)<br /><br />[Definir listas de teste para agrupar os testes](https://msdn.microsoft.com/library/dd286584(VS.100).aspx)|  
|**Fazer check-in dos projetos de teste e dos testes para controle de versão:** após executar os testes e verificar se estão funcionando corretamente, faça check-in do projeto de teste e de todos os arquivos associados para fazer o controle de versão, de modo que todos os membros da equipe possam executar os testes. Ao fazer check-in do seu projeto de teste em um controle de versão junto com seu projeto de banco de dados do SQL Server, você poderá facilmente restaurar as versões compatíveis dos testes de banco de dados e do seu banco de dados.|[Adicionar arquivos ao controle de versão](https://msdn.microsoft.com/library/ms181374(VS.100).aspx)<br /><br />[Usar as janelas Check-In e Alterações Pendentes](https://msdn.microsoft.com/library/ms245462(VS.100).aspx)|  
|**Definir condições de teste personalizadas:** você poderá criar condições de teste personalizadas se precisar testar o comportamento não abordado pelo conjunto padrão das condições de teste. Você deve distribuir essas condições para todos os membros da sua equipe que precisem executar os testes que usam as novas condições.|[Cenário: Definir condições de teste personalizadas para testes de unidade do SQL Server](https://msdn.microsoft.com/library/dd193282(VS.100).aspx)|  
|**Atualizar testes de unidade existentes:** se você tiver testes de unidade de banco de dados criados em uma versão anterior do Visual Studio, deverá atualizá-los antes que eles sejam criados e executados com êxito nessa versão.<br /><br />**OBSERVAÇÃO:** se você abrir uma solução que contém um projeto de banco de dados e um projeto de teste de unidade de banco de dados de uma versão anterior do Visual Studio, será solicitado a atualizar o projeto de banco de dados. Você não será solicitado a atualizar os projetos de testes de unidade de banco de dados, que deve ser atualizado manualmente.|[Atualizar um projeto de teste mais antigo contendo testes de unidade de banco de dados](../ssdt/upgrade-an-older-test-project-containing-database-unit-tests.md)|  
|**Extensibilidade:** você pode estender o SQL Server Data Tools criando extensões de recursos.|[Condições de teste personalizadas para testes de unidade do SQL Server](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)|  
|**Solucionar problemas:** você pode obter mais informações sobre como solucionar problemas comuns no teste de unidade do SQL Server.|[Solucionar problemas de teste de unidade do banco de dados SQL Server](../ssdt/troubleshooting-sql-server-database-unit-testing-issues.md)|  
  
## <a name="related-scenarios"></a>Cenários relacionados  
[Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md)  
O teste de unidade do banco de dados é particularmente eficaz quando for usado em conjunto com o desenvolvimento de projetos offline usando projetos de banco de dados do SQL Server.  
  
## <a name="see-also"></a>Consulte Também  
[SQL Server Data Tools](../ssdt/sql-server-data-tools.md)  
  
