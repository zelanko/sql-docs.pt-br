---
title: Introdução a este exemplo simples do Assistente de Importação e Exportação | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: quickstart
ms.assetid: ea3db39b-698b-4a74-8eb8-21dc7252dc1a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 40b71d77727435316c2595abba6db70119d4b152
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71285213"
---
# <a name="get-started-with-this-simple-example-of-the-import-and-export-wizard"></a>Introdução a este exemplo simples do Assistente de Importação e Exportação

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Saiba o que esperar do Assistente de Importação e Exportação do SQL Server examinando um cenário comum – a importação de dados de uma planilha do Excel para um banco de dados do SQL Server. Mesmo se você pretende usar uma fonte e um destino diferentes, este tópico mostra mais do que você precisa saber sobre como executar o assistente.

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>Pré-requisito – O assistente está instalado no computador?
Se você desejar executar o assistente, mas não tiver o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado no computador, será possível instalar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalando o SSDT (SQL Server Data Tools). Para obter mais informações, consulte [Baixar o SSDT (SQL Server Data Tools)](https://msdn.microsoft.com/library/mt204009.aspx).

## <a name="heres-the-excel-source-data-for-this-example"></a>Estes são os dados de origem do Excel para este exemplo
Estes são os dados de origem que você vai copiar – uma tabela pequena de duas colunas na planilha WizardWalkthrough da pasta de trabalho WizardWalkthrough.xlsx do Excel.

![Dados de origem do Excel](../../integration-services/import-export-data/media/excel-source-data.jpg)

## <a name="heres-the-sql-server-destination-database-for-this-example"></a>Este é o banco de dados de destino do SQL Server para este exemplo
Nele, (no SQL Server Management Studio) está o banco de dados de destino do SQL Server para o qual você vai copiar os dados de origem. A tabela de destino não existe – você vai deixar o assistente criar a tabela para você.

![Banco de dados de destino do SQL Server](../../integration-services/import-export-data/media/sql-server-destination-database.jpg)

## <a name="step-1---start-the-wizard"></a>Etapa 1 – Iniciar o assistente
Inicie o assistente no grupo do Microsoft SQL Server 2016 no menu Iniciar do Windows.

![Iniciar o assistente](../../integration-services/import-export-data/media/start-wizard.jpg)

> [!NOTE]
> Neste exemplo, você escolhe o assistente de 32 bits porque tem a versão de 32 bits do Microsoft Office instalada. Como resultado, você precisa usar o provedor de dados de 32 bits para se conectar ao Excel. Para muitas outras fontes de dados, normalmente, você pode escolher o assistente de 64 bits.
>
> Para usar a versão de 64 bits do Assistente de Importação e Exportação do SQL Server, você precisa instalar o SQL Server. O SSDT (SQL Server Data Tools) e o SSMS (SQL Server Management Studio) são aplicativos de 32 bits e somente instalam arquivos de 32 bits, incluindo a versão de 32 bits do assistente.

Para obter mais informações, consulte [Iniciar o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).

## <a name="step-2---view-the-welcome-page"></a>Etapa 2 – Exibir a página inicial
A primeira página do assistente é a página **inicial**. 

Provavelmente, você não deseja ver essa página novamente. Portanto, vá em frente e clique em **não mostrar esta página inicial novamente**.

![Bem-vindo ao assistente](../../integration-services/import-export-data/media/welcome-to-the-wizard.jpg)

## <a name="step-3---pick-excel-as-your-data-source"></a>Etapa 3 – Escolher o Excel como a fonte de dados
Na próxima página, **Escolher uma Fonte de Dados**, escolha o Microsoft Excel como a fonte de dados. Em seguida, procure para selecionar o arquivo do Excel. Finalmente, especifique a versão do Excel usada para criar o arquivo.

> [!IMPORTANT]
> Para obter informações detalhadas sobre como se conectar a arquivos do Excel, e sobre limitações e problemas conhecidos para carregar dados de ou para arquivos do Excel, consulte [Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md).

![Escolher a fonte de dados do Excel](../../integration-services/import-export-data/media/choose-the-excel-data-source.jpg)

Para obter mais informações sobre esta página do assistente, consulte [Escolher uma fonte de dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md).

## <a name="step-4---pick-sql-server-as-your-destination"></a>Etapa 4 – Escolher o SQL Server como o destino
Na próxima página, **Escolher um Destino**, escolha o Microsoft SQL Server como o destino selecionando um dos provedores de dados na lista que se conecta ao SQL Server. Neste exemplo, você escolhe o **Provedor de Dados .NET Framework para SQL Server**.

A página exibe uma lista de propriedades do provedor. Muitas delas são nomes não amigáveis e configurações desconhecidas. Felizmente, para se conectar a qualquer banco de dados empresarial, em geral, você precisa fornecer apenas três tipos de informação. Ignore os valores padrão para as outras configurações.

|Informações necessárias|Propriedade do Provedor de Dados do .NET Framework para SQL Server|
|---|---|
|Nome do servidor|**Fonte de Dados**|
|Informações (logon) de Autenticação|**Segurança Integrada**; ou **ID de Usuário** e **Senha**<br/>Se desejar ver uma lista suspensa de bancos de dados no servidor, primeiro precisará fornecer informações de logon válidas.|
|Nome do banco de dados|**Catálogo Inicial**|

![Escolher o destino do SQL Server](../../integration-services/import-export-data/media/choose-the-sql-server-destination.jpg)

Para obter mais informações sobre como se conectar ao SQL Server, consulte [Conectar-se a uma fonte de dados do SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md). Para obter mais informações sobre esta página do assistente, consulte [Escolher um destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md).

## <a name="step-5---copy-a-table-instead-of-writing-a-query"></a>Etapa 5 – Copiar uma tabela em vez de escrever uma consulta
Na próxima página, **Especificar Cópia de Tabela ou Consulta**, especifique que deseja copiar a tabela inteira de dados de origem. Você não deseja escrever uma consulta na linguagem SQL para selecionar os dados a serem copiados.

![Especificar para copiar uma tabela](../../integration-services/import-export-data/media/specify-to-copy-a-table.jpg)

Para obter mais informações sobre esta página do assistente, consulte [Especificar Cópia de Tabela ou Consulta](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md).

## <a name="step-6---pick-the-table-to-copy"></a>Etapa 6 – Escolher a tabela a ser copiada
Na próxima página, **Selecionar Tabelas de Origem e Exibições**, selecione as tabelas que deseja copiar da fonte de dados. Em seguida, mapeie cada tabela de origem selecionada para uma tabela de destino nova ou existente.

Neste exemplo, por padrão, o assistente mapeou a planilha **WizardWalkthrough$** na coluna **Origem** para uma nova tabela com o mesmo nome no destino do SQL Server. (A pasta de trabalho do Excel contém apenas uma única planilha.)
-   O cifrão ($) no nome da tabela de origem indica uma planilha do Excel. (Um intervalo nomeado no Excel é representado por seu nome apenas.)
-   A estrela no ícone da tabela de destino indica que o assistente vai criar uma nova tabela de destino.

![Selecionar a tabela (antes de renomear)](../../integration-services/import-export-data/media/select-the-table-before-renaming.jpg)

Provavelmente, você deseja remover o cifrão ($) do nome da nova tabela de destino.

![Selecionar a tabela (depois de renomear)](../../integration-services/import-export-data/media/select-the-table-after-renaming.jpg)

Para obter mais informações sobre esta página do assistente, consulte [Selecionar Tabelas de Origem e Exibições](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md).

## <a name="optional-step-7---review-the-column-mappings"></a>Etapa opcional 7 – Examinar os mapeamentos de coluna
Antes de sair da página **Selecionar Tabelas de Origem e Exibições**, opcionalmente, clique no botão **Editar Mapeamentos** para abrir a caixa de diálogo **Mapeamentos de Coluna**. Nela, na tabela **Mapeamentos**, você verá como o assistente vai mapear colunas na planilha de origem para colunas na nova tabela de destino.

![Exibir mapeamentos de coluna](../../integration-services/import-export-data/media/view-column-mappings.jpg)

Para obter mais informações sobre esta página do assistente, consulte [Mapeamentos de Coluna](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).

## <a name="optional-step-8---review-the-create-table-statement"></a>Etapa opcional 8 – Examinar a instrução CREATE TABLE
Enquanto a caixa de diálogo **Mapeamentos de Coluna** está aberta, opcionalmente, clique no botão **Editar SQL** para abrir a caixa de diálogo **Instrução SQL Create Table**. Nela, você verá a instrução **CREATE TABLE** gerada pelo assistente para criar a nova tabela de destino. Normalmente, você não precisa alterar a instrução.

![Exibir instrução CREATE TABLE](../../integration-services/import-export-data/media/view-create-table-statement.jpg)

Para obter mais informações sobre esta página do assistente, consulte [Instrução SQL Create Table](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md).

## <a name="optional-step-9---preview-the-data-to-copy"></a>Etapa opcional 9 – Visualizar os dados a serem copiados
Depois de clicar em **OK** para fechar a caixa de diálogo **Instrução SQL Create Table**, em seguida, clique em **OK** novamente para fechar a caixa de diálogo **Mapeamentos de Coluna**. Você retornará à página **Selecionar Tabelas de Origem e Exibições**. Opcionalmente, clique no botão **Visualizar** para ver uma amostra dos dados que o assistente vai copiar. Neste exemplo, eles parecem corretos.

![Visualizar dados a serem copiados](../../integration-services/import-export-data/media/preview-data-to-copy.jpg)

Para obter mais informações sobre esta página do assistente, consulte [Visualizar Dados](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).

## <a name="step-10---yes-you-want-to-run-the-import-export-operation"></a>Etapa 10 – Sim, você deseja executar a operação de importação/exportação
Na próxima página, **Salvar e Executar Pacote**, deixe a opção **Executar Imediatamente** habilitada para copiar os dados assim que você clicar em **Concluir** na próxima página. Outra alternativa é ignorar a próxima página clicando em **Concluir** na página **Salvar e Executar Pacote**.

![Executar o pacote](../../integration-services/import-export-data/media/run-the-package.jpg)

Para obter mais informações sobre essa página do assistente, consulte [Salvar e Executar Pacote](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).

## <a name="step-11---finish-the-wizard-and-run-the-import-export-operation"></a>Etapa 11 – Concluir o assistente e executar a operação de importação/exportação
Se você clicou em **Avançar** em vez de em **Concluir** na página **Salvar e Executar Pacote**, na próxima página, **Concluir o Assistente**, você verá um resumo do que o assistente vai fazer. Clique em **Concluir** para executar a operação de importação/exportação.

![Concluir o assistente](../../integration-services/import-export-data/media/complete-the-wizard.jpg)

Para obter mais informações sobre essa página do assistente, consulte [Concluir o Assistente](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).

## <a name="step-12---review-what-the-wizard-did"></a>Etapa 12 – Examinar as ações executadas pelo assistente
Na página final, observe o assistente concluir cada tarefa e, em seguida, examine os resultados. A linha realçada indica que o assistente copiou os dados com êxito. Você terminou!

![O assistente foi bem-sucedido](../../integration-services/import-export-data/media/the-wizard-succeeded.jpg)

Para obter mais informações sobre essa página do assistente, consulte [Executando a Operação](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md).

## <a name="heres-the-new-table-of-data-copied-to-sql-server"></a>Esta é a nova tabela de dados copiados para o SQL Server
Nele, (no SQL Server Management Studio), você verá a nova tabela de destino que o assistente criou no SQL Server.

![Dados copiados para o SQL Server](../../integration-services/import-export-data/media/data-copied-to-sql-server.jpg)

Nele, (novamente no SSMS), você verá os dados que o assistente copiou para o SQL Server.

![Dados copiados para o SQL Server 2](../../integration-services/import-export-data/media/data-copied-to-sql-server-2.jpg)

## <a name="learn-more"></a>Saiba mais  
Saiba mais sobre como o assistente funciona.
-   **Saiba mais sobre o assistente.** Se você estiver procurando uma visão geral sobre o assistente, consulte [Importar e Exportar Dados com o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

-   **Saiba mais sobre as etapas do assistente.** Se estiver procurando informações sobre as etapas do assistente, selecione a página desejada na lista aqui – [Etapas do Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md). Há também uma página separada da documentação para cada página do assistente.

-   **Saiba como se conectar a fontes de dados e destinos.** Se estiver procurando informações sobre como se conectar aos seus dados, selecione a página desejada na lista aqui – [Conectar-se a fontes de dados com o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md). Há uma página separada da documentação para cada uma das várias fontes de dados usadas com frequência.

-   **Saiba mais sobre como carregar dados de e para o Excel.** Se você estiver procurando informações sobre como se conectar a arquivos do Excel, e sobre limitações e problemas conhecidos para carregar dados de ou para arquivos do Excel, consulte [Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md).
