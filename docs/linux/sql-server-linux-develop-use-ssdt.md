---
title: Desenvolver e implantar bancos de dados SQL Server para Linux | Microsoft Docs
description: O SQL Server Data Tools com Visual Studio é um ambiente avançado de desenvolvimento e gerenciamento de ciclo de vida de banco de dados para SQL Server em Linux.
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1e924704-e07c-4a8b-b243-8c1dd8cff0d3
ms.openlocfilehash: dd4de5567d2bafd21b321dc388068b6ee6c24ed5
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92523911"
---
# <a name="use-visual-studio-to-create-databases-for-sql-server-on-linux"></a>Use o Visual Studio para criar bancos de dados para SQL Server em Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

O SSDT (SQL Server Data Tools) transforma o Visual Studio em um avançado ambiente de desenvolvimento e DLM (gerenciamento de ciclo de vida de banco de dados) para SQL Server em Linux. Você pode desenvolver, criar, testar e publicar seu banco de dados de um projeto de origem controlada. Como você desenvolve seu código de aplicativo.

## <a name="install-visual-studio-and-sql-server-data-tools"></a>Instalar o Visual Studio e o SQL Server Data Tools

1. Se você ainda não instalou o Visual Studio em seu computador Windows, [Baixe e instale o Visual Studio](https://visualstudio.microsoft.com/downloads/). Se você não tem uma licença do Visual Studio, o Visual Studio Community Edition é um IDE gratuito e completo para alunos, desenvolvedores individuais e de software livre.

2. Durante a instalação do Visual Studio, selecione **Personalizado** para a opção **Escolher o tipo de instalação** . Clique em **Avançar** .

3. Selecione **Microsoft SQL Server Data Tools** , **Git for Windows** e **Extensão do GitHub para Visual Studio** na lista seleção de recursos.

   <img src="./media/sql-server-linux-develop-use-ssdt/ssdt-setup.png" alt="ssdt setup" style="width: 400px;"/>

4. Continue e conclua a instalação do Visual Studio. Pode levar alguns minutos.

## <a name="upgrade-sql-server-data-tools-to-ssdt-170-rc-release"></a>Atualizar SQL Server Data Tools para a versão SSDT 17.0 RC

O SQL Server em Linux é compatível com o SSDT versão 17.0 RC ou posterior.

* [Baixar e instalar o SSDT 17.0 RC2](https://go.microsoft.com/fwlink/?linkid=837939).

## <a name="create-a-new-database-project-in-source-control"></a>Criar um novo projeto de banco de dados no controle do código-fonte

1. Inicie o Visual Studio.

2. Selecione **Team Explorer** no menu **Exibir** . 

3. Clique em **Novo** na seção **Repositório Git Local** na página **Conectar** .

   <img src="./media/sql-server-linux-develop-use-ssdt/git-repository.png" alt="Screenshot of the Local Git Repository section with the New option called out." style="width: 300px;"/>

4. Clique em **Criar** . Depois que o repositório Git local for criado, clique duas vezes em **SSDTRepo** .

5. Clique em **Novo** na seção **Soluções** . Selecione **SQL Server** no nó **Outras Linguagens** na caixa de diálogo **Novo Projeto** .

   <img src="./media/sql-server-linux-develop-use-ssdt/new-project.png" alt="Screenshot of the Solutions section with the New option and SQL Server option called out." style="width: 480px;"/>

6. Digite **TutorialDB** para o nome e clique em **OK** para criar um novo projeto de banco de dados.

## <a name="create-a-new-table-in-the-database-project"></a>Criar uma nova tabela no projeto de banco de dados

1. Selecione **Gerenciador de Soluções** no menu **Exibir** .

2. Abra o menu do projeto de banco de dados clicando com o botão direito do mouse em **TutorialDB** em Gerenciador de Soluções.

3. Selecione **Tabela** em **Adicionar** .

   <img src="./media/sql-server-linux-develop-use-ssdt/create-table.png" alt="create table" style="width: 480px;"/>

4. Usando o designer de tabela, adicione duas colunas, Nome `nvarchar(50)` e Localização `nvarchar(50)`, conforme mostrado na imagem. O SSDT gera o script `CREATE TABLE` à medida que você adiciona as colunas no designer.

   <img src="./media/sql-server-linux-develop-use-ssdt/add-columns.png" alt="Screenshot of the table designer with the Name and Location values called out." style="width: 480px;"/>

5. Salve o arquivo **Table1.sql** .

## <a name="build-and-validate-the-database"></a>Criar e validar o banco de dados

1. Abra o menu de projeto de banco de dados em **TutorialDB** e selecione **Compilar** . O SSDT compila arquivos de código-fonte .sql em seu projeto e cria um arquivo dacpac (pacote de Aplicativo da Camada de Dados). Isso pode ser usado para publicar um banco de dados em sua instância do SQL Server no Linux. 

   <img src="./media/sql-server-linux-develop-use-ssdt/build.png" alt="Screenshot showing the TutorialDB with the Build option called out." style="width: 400px;"/>

2. Verifique a mensagem sucesso do build na janela de **Saída** no Visual Studio. 

## <a name="publish-the-database-to-sql-server-instance-on-linux"></a>Publique o banco de dados para a instância do SQL Server no Linux

1. Abra o menu de projeto de banco de dados em **TutorialDB** e selecione **Publicar** .

2. Clique em **Editar** para selecionar sua instância de SQL Server no Linux.

   <img src="./media/sql-server-linux-develop-use-ssdt/publish-dialog.png" alt="publish dialog" style="width: 480px;"/>

3. Na caixa de diálogo de conexão, digite o endereço IP ou o nome do host de sua instância do SQL Server no Linux, nome de usuário e senha.

   <img src="./media/sql-server-linux-develop-use-ssdt/connection-dialog.png" alt="connection dialog" style="width: 400px;"/>

4. Clique no botão **Publicar** na caixa de diálogo Publicar.

5. Verifique o status de publicação na janela **Operações de Ferramentas de Dados** .

6. Clique em **Exibir Resultados** ou **Exibir Script** para ver detalhes do resultado da publicação do banco de dados em seu SQL Server em Linux.

   <img src="./media/sql-server-linux-develop-use-ssdt/publish-result.png" alt="publish result" style="width: 480px;"/>

Você criou com êxito um banco de dados na instância do SQL Server em Linux e aprendeu as noções básicas de como desenvolver um banco de dados com um projeto de banco de dados com controle do código-fonte.

## <a name="next-steps"></a>Próximas etapas

Se você for novo no T-SQL, confira o [Tutorial: Escrevendo instruções Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md).

Para obter mais informações sobre como desenvolver um banco de dados com SQL Data Tools, confira os artigos abaixo.

* [Baixar e instalar o Visual Studio](https://www.visualstudio.com/downloads/)
* [Baixar e instalar o SSDT](../ssdt/download-sql-server-data-tools-ssdt.md)
* [Documentos do MSDN do SSDT](/previous-versions/sql/sql-server-data-tools/hh272686(v=vs.103))
* [Tutorial: Gravando instruções Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md)
* [Referência do Transact-SQL (Mecanismo de Banco de Dados)](../t-sql/language-reference.md)