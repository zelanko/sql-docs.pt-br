---
title: Extensão de Projetos de Banco de Dados SQL
description: Instale e use a extensão de Projetos de Banco de Dados SQL (versão prévia) para Azure Data Studio
ms.custom: seodec18
ms.date: 07/30/2020
ms.reviewer: drskwier, maghan, sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 39ebf2d26e69e47edc700a489743d70762bef7b0
ms.sourcegitcommit: bf5acef60627f77883249bcec4c502b0205300a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88199989"
---
# <a name="sql-database-projects-extension-preview"></a>Extensão de Projetos de Banco de Dados SQL (versão prévia)

A extensão de Projetos do Banco de Dados SQL (versão prévia) é uma extensão para o desenvolvimento de Banco de Dados SQL em um ambiente de desenvolvimento baseado em projeto. Esta extensão está em versão prévia no momento e está disponível na [compilação interna do Azure Data Studio](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-main).


## <a name="features"></a>Recursos
1. Criar projeto a partir de um banco de dados conectado 
2. Criar um novo projeto em branco
3. Abra um projeto criado anteriormente no [Azure Data Studio](sql-database-project-extension-getting-started.md) ou no [SQL Server Data Tools](../ssdt/sql-server-data-tools.md) 
4. Editar projeto adicionando ou removendo Tabela, Exibição, Procedimento Armazenado ou scripts personalizados do projeto 
5. Organizar arquivos/scripts em pastas 
6. Adicionar referências a bancos de dados do sistema ou dacpac do usuário
7. Compilar projeto único 
8. Implantar projeto único
9. Carregar detalhes de conexão (autenticação do Windows para SQL) e variáveis SQLCMD a partir do perfil de implantação 

## <a name="install-the-sql-database-projects-extension"></a>Instalar a extensão de Projetos de Banco de Dados SQL

1. Abra o gerenciador de extensões para acessar as extensões disponíveis.  Para isso, selecione o ícone de extensões ou **Extensões** no menu **Exibir**.
2. Identificar a extensão de *Projetos de Banco de Dados SQL* digitando todo ou parte do nome na caixa de pesquisa de extensão. Selecione uma extensão disponível para exibir os detalhes.

   ![Instalar a extensão](media/extensions/sql-database-projects-extension/install-database-projects.png)

3. Selecione a extensão que você deseja e **Instale**-a.
4. Selecione **Recarregar** para habilitar a extensão (necessário apenas na primeira vez que você instala uma extensão).
5. Selecione o ícone arquivos na barra de atividade ou selecione **Explorer** no menu **Exibir**. Um novo viewlet de **Projetos** será disponibilizado.


   > [!NOTE]
   > O SDK do .NET Core é necessário para a funcionalidade de build do projeto, e será solicitada a instalação do SDK do .NET Core se a extensão não conseguir detectá-lo.  É possível baixar e instalar o SDK do .NET Core (v 3.1 ou posterior) em [https://dotnet.microsoft.com/download/dotnet-core/3.1](https://dotnet.microsoft.com/download/dotnet-core/3.1).

   > [!NOTE]
   > É recomendável instalar a [extensão de Comparação de Esquemas](schema-compare-extension.md) juntamente com a extensão de Projetos de Banco de Dados SQL para funcionalidade completa.

## <a name="known-limitations"></a>Limitações conhecidas
1. Atualmente, não há suporte para adicionar referências de projeto e carregar referências de projeto existentes na guia visualizadora do Azure Data Studio. 
2. Atualmente, não há suporte para o carregamento de arquivos como link na guia visualizadora do Azure Data Studio, mas os arquivos serão carregados no nível superior da árvore, e o build incorporará esses arquivos conforme o esperado. 
3. A partir de hoje, não há suporte para adicionar e carregar scripts de implantação pré-publicação na guia visualizadora, mas, se você adicionar manualmente esses arquivos no projeto, eles serão utilizados no momento do build. 
3. Na versão do .NET Core do DacFx, não há suporte para objetos SQLCLR no projeto. 
3. Tarefas (build/publicação) não são definidas pelo usuário
3. Publicar destinos definidos pelo DacFx
3. A integração de controle do código-fonte e a criação de projeto não criam automaticamente o arquivo .gitignore 
3. O suporte ao ambiente WSL é limitado 

## <a name="next-steps"></a>Próximas etapas
- [Introdução à extensão de Projetos de Banco de Dados SQL](sql-database-project-extension-getting-started.md)
- [Compilar e publicar um projeto com a extensão de Projetos de Banco de Dados SQL para Azure Data Studio](sql-database-project-extension-build.md)