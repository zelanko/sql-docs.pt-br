---
title: "Começar com esse exemplo simples de Assistente de importação e exportação | Microsoft Docs"
ms.custom: 
ms.date: 02/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: ea3db39b-698b-4a74-8eb8-21dc7252dc1a
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 1b59268e884d3e797a74ef65d9e75c405d75a0d5
ms.contentlocale: pt-br
ms.lasthandoff: 09/21/2017

---
# <a name="get-started-with-this-simple-example-of-the-import-and-export-wizard"></a>Começar com esse exemplo simples de Assistente de importação e exportação
Saiba o que esperar do SQL Server Assistente de importação e exportação examinando um cenário comum - importando dados de uma planilha do Excel para um banco de dados do SQL Server. Mesmo se você planeja usar uma fonte diferente e um destino diferente, este tópico mostra mais do que você precisa saber sobre como executar o assistente.

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>Pré - é o assistente instalado em seu computador?
Se você deseja executar o assistente, mas você não tiver [! INCLUIR[msCoName](/sql-docs/docs/ssdt/download-sql-server-data-tools-ssdt).

## <a name="heres-the-excel-source-data-for-this-example"></a>Eis os dados de origem do Excel para este exemplo
Aqui está a fonte de dados que você pretende copiar - uma pequena tabela de duas colunas na planilha da pasta de trabalho do WizardWalkthrough.xlsx Excel WizardWalkthrough.

![Dados de origem do Excel](../../integration-services/import-export-data/media/excel-source-data.jpg)

## <a name="heres-the-sql-server-destination-database-for-this-example"></a>Aqui está o banco de dados de destino do SQL Server para este exemplo
Aqui (no SQL Server Management Studio) é o banco de dados de destino do SQL Server ao qual você pretende copiar os dados de origem. A tabela de destino não estiver lá - você vai permitir que o assistente criar a tabela para você.

![Banco de dados de destino do SQL Server](../../integration-services/import-export-data/media/sql-server-destination-database.jpg)

## <a name="step-1---start-the-wizard"></a>Etapa 1: iniciar o Assistente
Inicie o Assistente do grupo Microsoft SQL Server 2016 no menu Iniciar do Windows.

![Iniciar o Assistente](../../integration-services/import-export-data/media/start-wizard.jpg)

> [!NOTE]
> Neste exemplo, você escolhe o Assistente de 32 bits porque você tem a versão de 32 bits do Microsoft Office instalado. Como resultado, você precisa usar o provedor de dados de 32 bits para se conectar ao Excel. Para muitas outras fontes de dados, normalmente você pode escolher o Assistente de 64 bits.
>
> Para usar a versão de 64 bits do SQL Server Assistente de importação e exportação, você precisa instalar o SQL Server. SQL Server Data Tools (SSDT) e SQL Server Management Studio (SSMS) são aplicativos de 32 bits, somente instalar os arquivos de 32 bits, incluindo a versão de 32 bits do assistente.

Para obter mais informações, consulte [Iniciar o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).

## <a name="step-2---view-the-welcome-page"></a>Etapa 2: exibir a página de boas-vinda
A primeira página do assistente é o **bem-vindo** página. 

Você provavelmente não deseja ver esta página novamente, então vá em frente e clique em **não mostrar esta página inicial novamente**.

![Bem-vindo ao Assistente](../../integration-services/import-export-data/media/welcome-to-the-wizard.jpg)

## <a name="step-3---pick-excel-as-your-data-source"></a>Etapa 3 - Pick Excel como fonte de dados
Na página seguinte, **escolher uma fonte de dados**, selecione Microsoft Excel como fonte de dados. Em seguida, navegue para selecionar o arquivo do Excel. Finalmente, você especifica a versão do Excel que você usou para criar o arquivo.

![Escolha a fonte de dados do Excel](../../integration-services/import-export-data/media/choose-the-excel-data-source.jpg)

Para obter mais informações sobre a conexão para o Excel, consulte [conectar-se a uma fonte de dados do Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md). Para obter mais informações sobre esta página do assistente, consulte [escolher uma fonte de dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md).

## <a name="step-4---pick-sql-server-as-your-destination"></a>Etapa 4 - Escolha como o destino do SQL Server
Na página seguinte, **escolha um destino**, selecione Microsoft SQL Server como seu destino selecionando um dos provedores de dados na lista que se conecta ao SQL Server. Neste exemplo, você escolhe o **.Net Framework Data Provider para SQL Server**.

A página exibe uma lista de propriedades do provedor. Esses são nomes amigáveis e configurações familiarizadas. Felizmente, para se conectar a qualquer banco de dados da empresa, geralmente você precisa fornecer apenas três partes de informações. Você pode ignorar os valores padrão para as outras configurações.

|Informações necessárias|.NET framework Data Provider para a propriedade do SQL Server|
|---|---|
|Nome do servidor|**Fonte de dados**|
|Informações de autenticação (logon)|**Segurança integrada**; ou **ID de usuário** e **senha**<br/>Se você quiser ver uma lista suspensa de bancos de dados no servidor, primeiro você precisa fornecer as informações de logon válido.|
|Nome do banco de dados|**Catálogo Inicial**|

![Escolha o destino do SQL Server](../../integration-services/import-export-data/media/choose-the-sql-server-destination.jpg)

Para obter mais informações sobre como se conectar ao SQL Server, consulte [conectar-se a uma fonte de dados do SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md). Para obter mais informações sobre esta página do assistente, consulte [escolha um destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md).

## <a name="step-5---copy-a-table-instead-of-writing-a-query"></a>Etapa 5: copiar uma tabela em vez de escrever uma consulta
Na página seguinte, **especificar cópia da tabela ou consulta**, especifique o que você deseja copiar a tabela inteira de dados de origem. Você não quiser escrever uma consulta em linguagem SQL para selecionar os dados a serem copiados.

![Especifique para copiar uma tabela](../../integration-services/import-export-data/media/specify-to-copy-a-table.jpg)

Para obter mais informações sobre esta página do assistente, consulte [especificar cópia da tabela ou consulta](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md).

## <a name="step-6---pick-the-table-to-copy"></a>Etapa 6 - Escolha a tabela a ser copiada
Na página seguinte, **selecionar tabelas de origem e exibições**, selecione a tabela ou tabelas que você deseja copiar da fonte de dados. Então, você deve mapear cada tabela de origem selecionada para uma tabela de destino de novo ou existente.

Neste exemplo, por padrão o assistente mapeou o **WizardWalkthrough$** planilha o **fonte** coluna para uma nova tabela com o mesmo nome no destino do SQL Server. (A pasta de trabalho do Excel contém apenas uma única planilha.)
-   O sinal de cifrão ($) no nome da tabela de origem indica uma planilha do Excel. (Nomeado no Excel alcance é representado por seu nome apenas.)
-   A forma de explosão no ícone de tabela de destino indica que o assistente irá criar uma nova tabela de destino.

![Selecione a tabela (antes de renomear)](../../integration-services/import-export-data/media/select-the-table-before-renaming.jpg)

Você provavelmente deseja remover o sinal de cifrão ($) do nome da nova tabela de destino.

![Selecione a tabela (depois de renomear)](../../integration-services/import-export-data/media/select-the-table-after-renaming.jpg)

Para obter mais informações sobre esta página do assistente, consulte [selecionar tabelas de origem e exibições](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md).

## <a name="optional-step-7---review-the-column-mappings"></a>Etapa opcional 7 - examine os mapeamentos de coluna
Antes de sair do **selecionar tabelas de origem e exibições** , opcionalmente, clique no **editar mapeamentos** para abrir o **mapeamentos de coluna** caixa de diálogo. Aqui, além de **mapeamentos** tabela, você verá como o assistente irá mapear colunas na planilha de origem para colunas na nova tabela de destino.

![Mapeamentos de coluna de exibição](../../integration-services/import-export-data/media/view-column-mappings.jpg)

Para obter mais informações sobre esta página do assistente, consulte [mapeamentos de coluna](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).

## <a name="optional-step-8---review-the-create-table-statement"></a>Etapa opcional 8 - examinar a instrução CREATE TABLE
Enquanto o **mapeamentos de coluna** caixa de diálogo está aberta, opcionalmente, clique no **Editar SQL** para abrir o **instrução Create Table SQL** caixa de diálogo. Veja o **CREATE TABLE** instrução gerada pelo Assistente para criar uma nova tabela de destino. Normalmente, você não precisa alterar a instrução.

![Instrução CREATE TABLE de exibição](../../integration-services/import-export-data/media/view-create-table-statement.jpg)

Para obter mais informações sobre esta página do assistente, consulte [instrução Create Table SQL](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md).

## <a name="optional-step-9---preview-the-data-to-copy"></a>Etapa opcional 9 - visualize os dados para copiar
Depois de clicar em **Okey** para fechar o **instrução Create Table SQL** caixa de diálogo caixa e, em seguida, clique em **Okey** novamente para fechar o **mapeamentos de coluna** caixa de diálogo, você está novamente o **selecionar tabelas de origem e exibições** página. Opcionalmente, clique no **visualização** botão para ver um exemplo dos dados que o assistente vai copiar. Neste exemplo, parece Okey.

![Visualização de dados para copiar](../../integration-services/import-export-data/media/preview-data-to-copy.jpg)

Para obter mais informações sobre esta página do assistente, consulte [visualizar dados](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).

## <a name="step-10---yes-you-want-to-run-the-import-export-operation"></a>Etapa 10 - Sim, você deseja executar a operação de importação-exportação
Na página seguinte, **salvar e executar pacote**, deixar **executar imediatamente** habilitado para copiar os dados assim que você clicar em **concluir** na próxima página. Ou você pode ignorar a próxima página, clicando em **concluir** no **salvar e executar pacote** página.

![Execute o pacote](../../integration-services/import-export-data/media/run-the-package.jpg)

Para obter mais informações sobre esta página do assistente, consulte [salvar e executar pacote](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).

## <a name="step-11---finish-the-wizard-and-run-the-import-export-operation"></a>Etapa 11 - concluir o assistente e execute a operação de importação-exportação
Se você clicou **próximo** em vez de **concluir** no **salvar e executar pacote** página, em seguida, na página seguinte, **concluir o assistente**, você ver um resumo do que o assistente está prestes a fazer. Clique em **concluir** para executar a operação de importação-exportação.

![Concluir o assistente](../../integration-services/import-export-data/media/complete-the-wizard.jpg)

Para obter mais informações sobre esta página do assistente, consulte [concluir o assistente](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).

## <a name="step-12---review-what-the-wizard-did"></a>Etapa 12 - examinar o que fez o Assistente
Na página final, observe que o Assistente para concluir cada tarefa e examine os resultados. A linha realçada indica que o assistente copiados com êxito seus dados. Terminar!

![O assistente foi bem-sucedida](../../integration-services/import-export-data/media/the-wizard-succeeded.jpg)

Para obter mais informações sobre esta página do assistente, consulte [executando operação](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md).

## <a name="heres-the-new-table-of-data-copied-to-sql-server"></a>Aqui está a nova tabela de dados copiados para o SQL Server
(No SQL Server Management Studio) veja a nova tabela de destino que o assistente criou no SQL Server.

![Dados copiados para o SQL Server](../../integration-services/import-export-data/media/data-copied-to-sql-server.jpg)

(Novamente, no SSMS) veja os dados que o assistente é copiado para o SQL Server.

![Dados copiados para o SQL Server 2](../../integration-services/import-export-data/media/data-copied-to-sql-server-2.jpg)

## <a name="learn-more"></a>Saiba mais  
Saiba mais sobre como funciona o assistente.
-   **Saiba mais sobre o assistente.** Se você estiver procurando uma visão geral sobre o assistente, consulte [Importar e Exportar Dados com o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

-   **Saiba mais sobre as etapas no assistente.** Se você estiver procurando informações sobre as etapas no assistente, selecione a página que você deseja na lista aqui - [as etapas no Assistente para exportação e do SQL Server Import](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md). Também é uma página separada da documentação de cada página do assistente.

-   **Saiba como se conectar a fontes de dados e destinos.** Se você estiver procurando informações sobre como conectar-se aos seus dados, selecione a página que você deseja na lista aqui - [conectar-se a fontes de dados com o SQL Server Assistente de importação e exportação](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md). Há uma página separada da documentação para cada uma das várias fontes de dados usadas com frequência.



