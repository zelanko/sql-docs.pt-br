---
title: Desenvolver e implantar o SQL Server bancos de dados para Linux | Microsoft Docs
description: ''
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1e924704-e07c-4a8b-b243-8c1dd8cff0d3
ms.openlocfilehash: 3981071bb6f175a130444dabc588d1dba18112f7
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833808"
---
# <a name="use-visual-studio-to-create-databases-for-sql-server-on-linux"></a>Use o Visual Studio para criar bancos de dados para o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server Data Tools (SSDT) transforma o Visual Studio em um poderoso ambiente de gerenciamento (DLM) do ciclo de vida de desenvolvimento e banco de dados para o SQL Server no Linux. Você pode desenvolver, criar, testar e publicar seu banco de dados de um projeto de controle do código-fonte, da mesma forma que você desenvolva o código do aplicativo.

## <a name="install-visual-studio-and-sql-server-data-tools"></a>Instalar o Visual Studio e o SQL Server Data Tools

1. Se você ainda não tiver instalado o Visual Studio em seu computador Windows, [baixar e instalar o Visual Studio]. Se você não tiver uma licença do Visual Studio, o Visual Studio Community edition é um IDE gratuito, completo para estudantes, desenvolvedores individuais e de código-fonte aberto.

2. Durante a instalação do Visual Studio, selecione **personalizado** para o **escolha o tipo de instalação** opção. Clique em **Avançar**.

3. Selecione **Microsoft SQL Server Data Tools**, **Git para Windows**, e **extensão GitHub para Visual Studio** da lista de seleção de recurso.

    <img src="./media/sql-server-linux-develop-use-ssdt/ssdt-setup.png" alt="ssdt setup" style="width: 400px;"/>

4. Continuar e concluir a instalação do Visual Studio. Ele pode levar alguns minutos.

## <a name="upgrade-sql-server-data-tools-to-ssdt-170-rc-release"></a>Atualizar o SQL Server Data Tools para a versão RC do SSDT 17.0

Há suporte para o SQL Server no Linux pelo SSDT versão 17.0 RC ou posterior.

* [Baixe e instale o SSDT 17.0 RC2](https://go.microsoft.com/fwlink/?linkid=837939).

## <a name="create-a-new-database-project-in-source-control"></a>Criar um novo projeto de banco de dados no controle de origem

1. Inicie o Visual Studio.

2. Selecione **Team Explorer** sobre o **exibição** menu. 

3. Clique em **New** na **repositório Git Local** seção os **Connect** página.

    <img src="./media/sql-server-linux-develop-use-ssdt/git-repository.png" alt="local repository" style="width: 300px;"/>

3. Clique em **Criar**. Depois que o repositório Git local é criado, clique duas vezes **SSDTRepo**.

4. Clique em **New** na **soluções** seção. Selecione **SQL Server** sob **outras linguagens** nó no **novo projeto** caixa de diálogo.

    <img src="./media/sql-server-linux-develop-use-ssdt/new-project.png" alt="local repository" style="width: 480px;"/>

5. Digite **TutorialDB** para o nome e clique **Okey** para criar um novo projeto de banco de dados.

## <a name="create-a-new-table-in-the-database-project"></a>Criar uma nova tabela no projeto de banco de dados

1. Selecione **Gerenciador de soluções** sobre o **exibição** menu.

2. Abra o menu de projeto de banco de dados, clicando duas vezes em **TutorialDB** no Gerenciador de soluções.

3. Selecione **tabela** sob **adicionar**.

    <img src="./media/sql-server-linux-develop-use-ssdt/create-table.png" alt="create table" style="width: 480px;"/>

4. Usando o designer de tabela, adicione duas colunas, nome `nvarchar(50)` e o local `nvarchar(50)`, conforme mostrado na imagem. SSDT gera o `CREATE TABLE` script conforme você adiciona as colunas no designer.

    <img src="./media/sql-server-linux-develop-use-ssdt/add-columns.png" alt="add columns" style="width: 480px;"/>

5. Salvar a **Table1.sql** arquivo.

## <a name="build-and-validate-the-database"></a>Compilar e validar o banco de dados

1. Abra o menu de projeto de banco de dados no **TutorialDB** e selecione **Build**. SSDT compila arquivos de código fonte. SQL em seu projeto e cria um arquivo de pacote (dacpac) do aplicativo da camada de dados. Isso pode ser usado para publicar um banco de dados em sua instância do SQL Server no Linux. 

    <img src="./media/sql-server-linux-develop-use-ssdt/build.png" alt="add columns" style="width: 400px;"/>

2. Fazer check-in de mensagem de sucesso de build **saída** janela no Visual Studio. 

## <a name="publish-the-database-to-sql-server-instance-on-linux"></a>Publicar o banco de dados à instância do SQL Server no Linux

1. Abra o menu de projeto de banco de dados no **TutorialDB** e selecione **publicar**.

2. Clique em **editar** para selecionar a instância do SQL Server no Linux.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-dialog.png" alt="publish dialog" style="width: 480px;"/>

3. Na caixa de diálogo de conexão, digite o nome de host ou endereço IP da sua instância do SQL Server no Linux, o nome de usuário e senha.

    <img src="./media/sql-server-linux-develop-use-ssdt/connection-dialog.png" alt="connection dialog" style="width: 400px;"/>

4. Clique o **publicar** botão na caixa de diálogo Publicar.

5. Verifique o status de publicação no **operações de ferramentas de dados** janela.

6. Clique em **exibir resultados** ou **Exibir Script** para ver os detalhes do banco de dados a publicar resultados no SQL Server no Linux.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-result.png" alt="publish result" style="width: 480px;"/>

Você criou um novo banco de dados na instância do SQL Server no Linux e aprendeu os fundamentos do desenvolvimento de um banco de dados com um projeto de banco de dados de controle do código-fonte com êxito.

## <a name="next-steps"></a>Próximas etapas

Se você for novo no T-SQL, consulte [Tutorial: Gravando instruções Transact-SQL] e o [referência de Transact-SQL (mecanismo de banco de dados)].

Para obter mais informações sobre o desenvolvimento de um banco de dados com ferramentas de dados SQL, consulte [Documentos do SSDT MSDN]

[Baixar e instalar o Visual Studio]: https://www.visualstudio.com/downloads/
[Download and Install SSDT]:https://aka.ms/ssdt-download
[Documentos do SSDT MSDN]: https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx
[Tutorial: Gravando instruções Transact-SQL]: https://msdn.microsoft.com/library/ms365303.aspx
[Referência de Transact-SQL (mecanismo de banco de dados)]: https://msdn.microsoft.com/library/bb510741.aspx
