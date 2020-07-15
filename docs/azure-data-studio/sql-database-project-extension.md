---
title: Extensão de Projetos de Banco de Dados SQL
description: Instale e use a extensão de Projetos de Banco de Dados SQL (versão prévia) para Azure Data Studio
ms.custom: seodec18
ms.date: 06/25/2020
ms.reviewer: drskwier, maghan, sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 609af04cec2f6eaaaf1890e19c6d85fbd4bd5b8a
ms.sourcegitcommit: b860fe41b873977649dca8c1fd5619f294c37a58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2020
ms.locfileid: "85519140"
---
# <a name="sql-database-projects-extension-preview"></a>Extensão de Projetos de Banco de Dados SQL (versão prévia)

A extensão de Projetos do Banco de Dados SQL (versão prévia) é uma extensão para o desenvolvimento de Banco de Dados SQL em um ambiente de desenvolvimento baseado em projeto. Esta extensão está em versão prévia no momento e está disponível na [compilação interna do Azure Data Studio](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-main).


## <a name="install-the-sql-database-projects-extension"></a>Instalar a extensão de Projetos de Banco de Dados SQL

1. Para abrir o gerenciador de extensões e acessar as extensões disponíveis, selecione o ícone de extensões ou selecione **Extensões** no menu **Exibir**.
2. Identificar a extensão de *Projetos de Banco de Dados SQL* digitando todo ou parte do nome na caixa de pesquisa de extensão. Selecione uma extensão disponível para exibir os detalhes.

   ![Instalar a extensão](media/extensions/sql-database-projects-extension/install-database-projects.png)

3. Selecione a extensão que você deseja e **Instale**-a.
4. Selecione **Recarregar** para habilitar a extensão (necessário apenas na primeira vez que você instala uma extensão).
5. Selecione o ícone arquivos na barra de atividade ou selecione **Explorer** no menu **Exibir**. Um novo viewlet de **Projetos** será disponibilizado.

   > [!NOTE]
   > É recomendável instalar a [extensão de Comparação de Esquemas](schema-compare-extension.md) juntamente com a extensão de Projetos de Banco de Dados SQL para funcionalidade completa.

## <a name="getting-started-with-database-projects"></a>Introdução aos Projetos de Banco de Dados

* Crie um projeto de banco de dados acessando o viewlet de **Projetos** no Explorer ou procurando por **Novo projeto de banco de dados** na paleta de comandos.
* Os projetos de banco de dados existentes podem ser abertos por meio da opção **Abrir Projeto de Banco de Dados** da paleta de comandos.
* Inicie de um banco de dados existente usando **Importar Novo Projeto de Banco de Dados** da paleta de comandos.

   ![Novo viewlet](media/extensions/sql-database-projects-extension/projects-viewlet.png)


### <a name="create-an-empty-database-project"></a>Criar um Projeto de Banco de Dados Vazio

 No viewlet **Projetos**, em **Explorer**, clique no botão **Novo Projeto** e insira um nome de projeto na entrada de texto exibida.  Na caixa de diálogo "Selecionar uma pasta" exibida, selecione um diretório para armazenar a pasta do projeto, o arquivo.sqlproj e outros conteúdos.
O projeto vazio será aberto e ficará visível no viewlet **Projetos** para edição.

### <a name="open-an-existing-project"></a>Abrir um projeto existente

No viewlet **Projetos**, clique no botão **Abrir projeto** e abra um arquivo *.sqlproj* existente no seletor de arquivos exibido. Os projetos existentes podem ser originados no Azure Data Studio ou nas [SQL Server Data Tools do Visual Studio](../ssdt/sql-server-data-tools.md).

O projeto existente será aberto e o seu conteúdo fica visível no viewlet **Projetos** para edição.

### <a name="create-a-database-project-from-an-existing-database"></a>Criar um Projeto de Banco de Dados com base em um Banco de Dados Existente

No viewlet **Projeto**, clique no botão **Importar projeto do banco de dados** e conecte-se a um SQL Server.  Depois que a conexão for estabelecida, selecione um banco de dados na lista de bancos de dados disponíveis e defina o nome do projeto.

Por fim, selecione uma estrutura de destino para a extração.  O novo projeto será aberto e conterá scripts SQL para o conteúdo do banco de dados selecionado.

## <a name="build-and-publish"></a>Compilar e publicar

A implantação do projeto de banco de dados é alcançada na extensão de Projetos de Banco de Dados SQL para Azure Data Studio por meio da compilação do projeto em um [DACPAC](../relational-databases/data-tier-applications/data-tier-applications.md) (arquivo de aplicativo da camada de dados) e da publicação em uma plataforma compatível. Para obter mais informações sobre esse processo, confira [Compilar e publicar um projeto](sql-database-project-extension-build.md).

## <a name="schema-compare"></a>Comparação de Esquemas
A extensão de Projetos de Banco de Dados SQL interage com a [extensão de Comparação de Esquemas](schema-compare-extension.md), se instalada, para comparar o conteúdo de um projeto com um dacpac ou um banco de dados existente.  A comparação de esquemas resultante pode ser usada para exibir e aplicar as diferenças da origem ao destino.

## <a name="next-steps"></a>Próximas etapas

- [Compilar e publicar um projeto com a extensão de Projetos de Banco de Dados SQL para Azure Data Studio](sql-database-project-extension-build.md)
- [Aplicativos da camada de dados](../relational-databases/data-tier-applications/data-tier-applications.md)