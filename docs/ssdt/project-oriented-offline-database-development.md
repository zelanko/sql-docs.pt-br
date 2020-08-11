---
title: Desenvolvimento de banco de dados offline orientado a projetos
description: Veja os recursos disponíveis sobre tarefas de desenvolvimento de banco de dados offline orientadas a projetos, como a importação de objetos em um banco de dados e o uso de objetos de sequência.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.dbprojectwizard.general
- sql.data.tools.dbprojectwizard.summary
ms.assetid: e61e830d-9fcd-45e7-b7b4-93a42155dd56
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 5e56a458d06fbc70a71f36f87fdcd68bd8688847
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896613"
---
# <a name="project-oriented-offline-database-development"></a>Desenvolvimento de banco de dados offline orientado a projetos

Esta seção descreve os recursos fornecidos pelo SSDT (SQL Server Data Tools) para criar, compilar, depurar e publicar um projeto de banco de dados.  
  
Usando o SSDT, você pode criar um projeto de banco de dados offline e implementar alterações de esquema adicionando, modificando ou excluindo as definições de objetos (representadas por scripts) no projeto, sem uma conexão com uma instância do servidor. Todas essas ações podem ser realizadas usando o designer de tabela ou o Editor Transact\-SQL. Você também pode gravar e depurar objetos Transact\-SQL e CLR no mesmo projeto. Você pode usar a Comparação de Esquemas para garantir que seu projeto esteja sincronizado com o banco de dados de produção, e criar instantâneos para o projeto em cada fase do ciclo de desenvolvimento para fins de comparação. Enquanto você estiver trabalhando em seus projetos de banco de dados em um ambiente baseado em equipe, pode empregar controle de versão para todos os arquivos. Depois que seu projeto de banco de dados tiver sido desenvolvido, testado e depurado, você poderá entregá-lo à equipe autorizada para ser publicado em um ambiente de produção.  
  
> [!NOTE]  
> Os tópicos de instruções nesta seção contêm uma série de tarefas que podem ser realizadas em uma sequência.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|---------|---------------|  
|[Importar para um projeto de banco de dados](../ssdt/import-into-a-database-project.md)|Descreve como importar objetos de um banco de dados dinâmico, .dacpac ou script.|  
|[Caixa de diálogo Adicionar referência de banco de dados](../ssdt/add-database-reference-dialog-box.md)|Descreve várias formas de adicionar uma referência de banco de dados.|  
|[Caixa de diálogo Verificar atualizações](../ssdt/check-for-updates-dialog-box.md)|Descreve como o SQL Server Data Tools pode verificar atualizações do produto.|  
|[Configurações de projeto de banco de dados](../ssdt/database-project-settings.md)|Descreve várias configurações de projeto para controlar os aspectos do seu banco de dados e criar configurações.|  
|[Como: procurar objetos em um projeto de banco de dados do SQL Server](../ssdt/how-to-browse-objects-in-a-sql-server-database-project.md)|O Pesquisador de Objetos do SQL Server no Visual Studio agora contém um nó Projetos dedicado, sob o qual todos os projetos de bancos de dados do SQL Server em sua solução são agrupados em uma hierarquia semelhante à do SQL Server Management Studio.|  
|[Janela Operações de ferramentas de dados](../ssdt/data-tools-operations-window.md)|Descreve a janela **Operações de Ferramentas de Dados** , que mostra o progresso de algumas operações e notifica sobre erros.|  
|[Opções do Editor Transact-SQL](../ssdt/transact-sql-editor-options.md)|Descreve as opções do Transact\-SQL.|  
|[Como: Criar um projeto de banco de dados](../ssdt/how-to-create-a-new-database-project.md)|Crie um projeto de banco de dados e importe o esquema de banco de dados existente.|  
|[Como: Usar comparação de esquema para comparar definições de banco de dados diferentes](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)|Compare os esquemas de um banco de dados e um projeto e sincronize-os.|  
|[Como: Criar e implantar em um banco de dados local](../ssdt/how-to-build-and-deploy-to-a-local-database.md)|Use a instância local do SQL Server sob demanda, que é ativada quando um projeto de banco de dados é depurado.|  
|[Como: Alterar a plataforma de destino e publicar um projeto de banco de dados](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)|Altere a plataforma SQL Server de destino do seu projeto para qualquer instância com suporte do SQL Server e valide a sintaxe.|  
|[Como: Criar um instantâneo de um projeto](../ssdt/how-to-create-a-snapshot-of-a-project.md)|Crie um proxy somente leitura do esquema de banco de dados e reverta o projeto de origem quando são aplicadas alterações indesejáveis ao projeto.|  
|[Como: Usar objetos do Microsoft SQL Server 2012 no seu projeto](../ssdt/how-to-use-microsoft-sql-server-2012-objects-in-your-project.md)|Adicione um novo objeto de sequência a seu projeto.|  
|[Como: Trabalhar com objetos de banco de dados CLR](../ssdt/how-to-work-with-clr-database-objects.md)|Crie e publique objetos CLR no projeto de banco de dados do SQL Server Data Tools.|  
|[Como: Converter projetos de banco de dados do Visual Studio 2010 em projetos de banco de dados do SQL Server e redirecionar para uma plataforma diferente](../ssdt/how-to-convert-visual-studio-2010-database-projects-to-ssql-server-projects.md)|Converta projetos existentes de Banco de Dados, objetos CLR e Aplicativo da Camada de Dados do SQL Server criados no Visual Studio 2010 no projeto de banco de dados do SQL Server Data Tools.|  
|[Como: Especificar scripts de pré-implantação ou pós-implantação](../ssdt/how-to-specify-predeployment-or-postdeployment-scripts.md)|Discute como usar scripts que você quer executar antes ou após a implantação de seu banco de dados.|  
  
## <a name="related-sections"></a>Seções relacionadas

[Gerenciar tabelas, relações e corrigir erros](../ssdt/manage-tables-relationships-and-fix-errors.md)
