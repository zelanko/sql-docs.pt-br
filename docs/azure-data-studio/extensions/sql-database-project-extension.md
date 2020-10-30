---
title: Extensão de Projetos de Banco de Dados SQL
description: Instale e use a extensão Projetos de Banco de Dados SQL para o Azure Data Studio.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: ''
ms.date: 10/22/2020
ms.openlocfilehash: bd361913ac7f094e217b6b75163a0dd96d97d7e2
ms.sourcegitcommit: d35d0901296580bfceda6e0ab2e14cf2b7e99a0f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92496739"
---
# <a name="sql-database-projects-extension-preview"></a>Extensão de Projetos de Banco de Dados SQL (versão prévia)

A extensão de Projetos do Banco de Dados SQL (versão prévia) é uma extensão para o desenvolvimento de Banco de Dados SQL em um ambiente de desenvolvimento baseado em projeto. 


## <a name="features"></a>Recursos

1. Criar projeto em um banco de dados conectado.
2. Criar um projeto em branco.
3. Abrir um projeto criado anteriormente no [Azure Data Studio](sql-database-project-extension-getting-started.md) ou no [SQL Server Data Tools](../../ssdt/sql-server-data-tools.md).
4. Editar o projeto adicionando ou removendo uma Tabela, uma Exibição, um Procedimento Armazenado ou scripts personalizados do projeto.
5. Organizar arquivos/scripts em pastas.
6. Adicionar referências a bancos de dados do sistema ou dacpac do usuário.
7. Compilar projeto único.
8. Implantar projeto único.
9. Carregar detalhes de conexão (autenticação do Windows para SQL) e variáveis SQLCMD usando o perfil de implantação.

Assista a este vídeo rápido de 10 minutos para obter uma introdução à extensão de Projetos do Banco de Dados SQL no Azure Data Studio:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Build-SQL-Database-Projects-Easily-in-Azure-Data-Studio/player?WT.mc_id=dataexposed-c9-niner]

## <a name="install-the-sql-database-projects-extension"></a>Instalar a extensão de Projetos de Banco de Dados SQL

1. Abra o gerenciador de extensões para acessar as extensões disponíveis.  Para isso, selecione o ícone de extensões ou **Extensões** no menu **Exibir** .
2. Identificar a extensão de *Projetos de Banco de Dados SQL* digitando todo ou parte do nome na caixa de pesquisa de extensão. Selecione uma extensão disponível para exibir os detalhes.

   ![Instalar a extensão](media/sql-database-projects-extension/install-database-projects.png)

3. Selecione a extensão que você deseja e **Instale** -a.
4. Selecione **Recarregar** para habilitar a extensão (necessário apenas na primeira vez que você instala uma extensão).
5. Selecione o ícone arquivos na barra de atividade ou selecione **Explorer** no menu **Exibir** . Um novo viewlet de **Projetos** será disponibilizado.

   > [!NOTE]
   > O SDK do .NET Core é necessário para a funcionalidade de build do projeto, e será solicitada a instalação do SDK do .NET Core se a extensão não conseguir detectá-lo.  É possível baixar e instalar o SDK do .NET Core (v 3.1 ou posterior) em [https://dotnet.microsoft.com/download/dotnet-core/3.1](https://dotnet.microsoft.com/download/dotnet-core/3.1).

   > [!NOTE]
   > É recomendável instalar a [extensão de Comparação de Esquemas](schema-compare-extension.md) juntamente com a extensão de Projetos de Banco de Dados SQL para funcionalidade completa.

## <a name="known-limitations"></a>Limitações conhecidas

1. Atualmente, não há suporte para adicionar referências de projeto e carregar referências de projeto existentes na guia visualizadora do Azure Data Studio.
2. Atualmente, não há suporte para o carregamento de arquivos como link na guia visualizadora do Azure Data Studio, mas os arquivos serão carregados no nível superior da árvore, e o build incorporará esses arquivos conforme o esperado.
3. A partir de hoje, não há suporte para adicionar e carregar scripts de implantação pré-publicação na guia visualizadora, mas, se você adicionar manualmente esses arquivos no projeto, eles serão utilizados no momento do build.
4. Na versão do .NET Core do DacFx, não há suporte para objetos SQLCLR no projeto.
5. Tarefas (build/publicação) não são definidas pelo usuário.
6. Destinos de publicação são definidos pelo DacFx.
7. A integração de controle do código-fonte e a criação de projeto não criam automaticamente o arquivo .gitignore.
8. O suporte ao ambiente WSL é limitado.

## <a name="next-steps"></a>Próximas etapas

- [Introdução à extensão de Projetos de Banco de Dados SQL](sql-database-project-extension-getting-started.md)
- [Compilar e publicar um projeto com a extensão de Projetos de Banco de Dados SQL para Azure Data Studio](sql-database-project-extension-build.md)
