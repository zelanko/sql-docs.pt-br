---
title: Desenvolver e implantar o SQL Server bancos de dados para Linux | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: 1e924704-e07c-4a8b-b243-8c1dd8cff0d3
ms.custom: sql-linux
ms.openlocfilehash: efc03030c4d0c329fa7736e3622c621f684eecb3
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="use-visual-studio-to-create-databases-for-sql-server-on-linux"></a>Use o Visual Studio para criar bancos de dados para SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server Data Tools (SSDT) transforma o Visual Studio em um ambiente de gerenciamento (DLM) de ciclo de vida de desenvolvimento e banco de dados avançado para o SQL Server no Linux. Você pode desenvolver, compilar, testar e publicar o banco de dados de um projeto de controle do código-fonte, exatamente como você desenvolver o código do aplicativo.

## <a name="install-visual-studio-and-sql-server-data-tools"></a>Instalar o Visual Studio e SQL Server Data Tools

1. Se você ainda não tiver instalado o Visual Studio em seu computador Windows, [Baixar e instalar o Visual Studio]. Se você não tiver uma licença do Visual Studio, o Visual Studio Community edition é um IDE livre, completa para estudantes, os desenvolvedores de código-fonte aberto e individuais.

2. Durante a instalação do Visual Studio, selecione **personalizado** para o **escolha o tipo de instalação** opção. Clique em **Avançar**.

3. Selecione **Microsoft SQL Server Data Tools**, **Git para Windows**, e **extensão GitHub para Visual Studio** da lista de seleção de recurso.

    <img src="./media/sql-server-linux-develop-use-ssdt/ssdt-setup.png" alt="ssdt setup" style="width: 400px;"/>

4. Continuar e concluir a instalação do Visual Studio. Pode levar alguns minutos.

## <a name="upgrade-sql-server-data-tools-to-ssdt-170-rc-release"></a>Atualizar o SQL Server Data Tools para versão do SSDT 17.0 RC

2017 do SQL Server no Linux há suporte pelo SSDT versão 17.0 RC ou posterior.

* [Baixar e instalar o SSDT 17.0 RC2](https://go.microsoft.com/fwlink/?linkid=837939).

## <a name="create-a-new-database-project-in-source-control"></a>Criar um novo projeto de banco de dados no controle do código-fonte

1. Inicie o Visual Studio.

2. Selecione **Team Explorer** no **exibição** menu. 

3. Clique em **novo** na **repositório Git Local** seção o **conectar** página.

    <img src="./media/sql-server-linux-develop-use-ssdt/git-repository.png" alt="local repository" style="width: 300px;"/>

3. Clique em **Criar**. Depois que o repositório Git local é criado, clique duas vezes em **SSDTRepo**.

4. Clique em **novo** no **soluções** seção. Selecione **do SQL Server** em **outras linguagens** nó o **novo projeto** caixa de diálogo.

    <img src="./media/sql-server-linux-develop-use-ssdt/new-project.png" alt="local repository" style="width: 480px;"/>

5. Digite **TutorialDB** para o nome e clique em **Okey** para criar um novo projeto de banco de dados.

## <a name="create-a-new-table-in-the-database-project"></a>Criar uma nova tabela no projeto de banco de dados

1. Selecione **Solution Explorer** no **exibição** menu.

2. Abra o menu de projeto de banco de dados clicando em **TutorialDB** no Gerenciador de soluções.

3. Selecione **tabela** em **adicionar**.

    <img src="./media/sql-server-linux-develop-use-ssdt/create-table.png" alt="create table" style="width: 480px;"/>

4. Usando o designer de tabela, adiciona duas colunas, nome `nvarchar(50)` e local `nvarchar(50)`, conforme mostrado na imagem. SSDT gera o `CREATE TABLE` script conforme você adiciona as colunas no designer.

    <img src="./media/sql-server-linux-develop-use-ssdt/add-columns.png" alt="add columns" style="width: 480px;"/>

5. Salve o **Table1.sql** arquivo.

## <a name="build-and-validate-the-database"></a>Criar e validar o banco de dados

1. Abra o menu de projeto de banco de dados em **TutorialDB** e selecione **criar**. SSDT compila arquivos em seu projeto de código-fonte. SQL e cria um arquivo de pacote (dacpac) do aplicativo da camada de dados. Isso pode ser usado para publicar um banco de dados à instância do SQL Server 2017 no Linux. 

    <img src="./media/sql-server-linux-develop-use-ssdt/build.png" alt="add columns" style="width: 400px;"/>

2. Verifique a mensagem de êxito de compilação **saída** janela no Visual Studio. 

## <a name="publish-the-database-to-sql-server-2017-instance-on-linux"></a>Publicar o banco de dados à instância do SQL Server 2017 no Linux

1. Abra o menu de projeto de banco de dados em **TutorialDB** e selecione **publicar**.

2. Clique em **editar** para selecionar a instância do SQL Server no Linux.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-dialog.png" alt="publish dialog" style="width: 480px;"/>

3. Na caixa de diálogo conexão, digite o nome de host ou endereço IP da sua instância do SQL Server no Linux, o nome de usuário e senha.

    <img src="./media/sql-server-linux-develop-use-ssdt/connection-dialog.png" alt="connection dialog" style="width: 400px;"/>

4. Clique o **publicar** botão na caixa de diálogo Publicar.

5. Verifique o status da publicação **operações de ferramentas de dados** janela.

6. Clique em **exibição Reulst** ou **Exibir Script** para ver os detalhes do banco de dados a publicar os resultados no SQL Server no Linux.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-result.png" alt="publish result" style="width: 480px;"/>

Você criou um novo banco de dados na instância do SQL Server no Linux e aprendeu as Noções básicas de desenvolvimento de um banco de dados com um projeto de banco de dados de controle do código-fonte com êxito.

## <a name="next-steps"></a>Próximas etapas

Se você estiver familiarizado com o T-SQL, consulte [Tutorial: Gravando instruções Transact-SQL] e [Referência do Transact-SQL (mecanismo de banco de dados)].

Para obter mais informações sobre como desenvolver um banco de dados com as ferramentas de dados SQL, consulte [documentos do MSDN do SSDT]

[Baixar e instalar o Visual Studio]:https://www.visualstudio.com/downloads/
[Download and Install SSDT 17.0 RC2]:https://aka.ms/ssdt-download
[Documentos do MSDN do SSDT]: https://msdn.microsoft.com/en-us/library/hh272686(v=vs.103).aspx
[Tutorial: Gravando instruções Transact-SQL]:https://msdn.microsoft.com/library/ms365303.aspx
[Referência do Transact-SQL (mecanismo de banco de dados)]:https://msdn.microsoft.com/library/bb510741.aspx
