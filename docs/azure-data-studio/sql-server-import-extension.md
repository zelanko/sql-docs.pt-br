---
title: Extensão de importação do SQL Server
titleSuffix: Azure Data Studio
description: Instalar e usar a extensão de importação do SQL Server (versão prévia) para o Studio de dados do Azure
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 8248404353674f8139a26cfc75f37363557136b9
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030740"
---
# <a name="sql-server-import-extension-preview"></a>Extensão de importação do SQL Server (versão prévia)

A extensão de importação do SQL Server (versão prévia) converte arquivos. txt e. csv em uma tabela SQL. Este assistente utiliza uma estrutura do Microsoft Research conhecida como [Program Synthesis using exemplos (PROSA)](https://microsoft.github.io/prose/) inteligentemente analisar o arquivo com a entrada do usuário mínima. É uma estrutura poderosa para disputa de dados, e é a mesma tecnologia que alimenta o Flash Fill no Microsoft Excel

Para saber mais sobre a versão do SSMS desse recurso, você pode ler [deste artigo](https://docs.microsoft.com/sql/relational-databases/import-export/import-flat-file-wizard).


## <a name="install-the-sql-server-import-extension"></a>Instalar a extensão de importação do SQL Server

1. Para abrir o Gerenciador de extensões e acessar as **extensões** disponíveis, selecione o ícone de extensões ou selecione extensões no menu **Exibição**.
2. Selecione uma extensão disponível para exibir seus detalhes.

   ![Gerenciador de extensões de importação](media/sql-server-import-extension/import-wizard-install.png)

1. Selecione a extensão desejada e **instale-a**.
2. Selecione **Recarregar** para habilitar a extensão (necessário somente na primeira vez que você instalar uma extensão).

## <a name="start-import-wizard"></a>Iniciar Assistente de importação

1. Para iniciar o SQL Server Import, fazer uma conexão a um servidor na guia servidores.
2. Depois de fazer uma conexão, fazer drill down até o banco de dados de destino que você deseja importar um arquivo para uma tabela SQL.
3. Clique com botão direito no banco de dados e clique em **Assistente de importação**.
    ![Assistente de importação aberto](media/sql-server-import-extension/open-import-wizard.png)

## <a name="importing-a-file"></a>Importando um arquivo
1. Quando o botão direito do mouse para iniciar o assistente, o servidor e o banco de dados são já automaticamente preenchidas. Se houver outras conexões ativas, você pode selecionar na lista suspensa. 
    
    Selecione um arquivo, clicando em **procurar.** Ele deve preencher automaticamente o nome da tabela com base no nome do arquivo, mas você também pode alterá-lo por conta própria.

    Por padrão, o esquema será o dbo, mas você pode alterá-lo. Clique em **Avançar** para continuar.
    ![arquivo de entrada](media/sql-server-import-extension/import-wizard-input-file.png)
1. O assistente irá gerar uma visualização com base nas primeiras 50 linhas. Não há nenhuma ação adicional nesta página em vez de verificar que os dados serão precisos. Clique em **Avançar** para continuar.
    ![Assistente de importação aberto](media/sql-server-import-extension/import-wizard-preview-data.png)
2. Nessa página, você pode fazer alterações para o nome da coluna de tipo de dados, se ele é uma chave primária ou permitir valores nulos. Você pode fazer alterações de quantos desejar. Clique em **importação de dados** para continuar.
    ![Assistente de importação aberto](media/sql-server-import-extension/import-wizard-modify-columns.png)
3. Esta página fornece um resumo das ações escolhido. Você também pode ver se sua tabela inserida com êxito ou não. 

    Você pode clicar em **feito,** **Previous** se você precisar fazer alterações, ou **novo arquivo de importação** para importar rapidamente outro arquivo.
    ![Assistente de importação aberto](media/sql-server-import-extension/import-wizard-summary.png)
1. Verifique se sua tabela importados com êxito a atualização de seu banco de dados de destino ou executando uma consulta SELECT no nome da tabela.

## <a name="next-steps"></a>Próximas etapas
- Para saber mais sobre o Assistente de importação, leia as [postagem de blog](https://cloudblogs.microsoft.com/sqlserver/2018/08/30/the-august-release-of-sql-operations-studio-is-now-available/).
- Para saber mais sobre o PROSE, leia o [documentação.](https://microsoft.github.io/prose/)
