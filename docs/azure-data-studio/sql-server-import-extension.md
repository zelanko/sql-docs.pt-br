---
title: Extensão de Importação do SQL Server
description: Saiba como instalar e usar a extensão de importação do SQL Server (versão prévia) para o Azure Data Studio, um assistente que converte arquivos .txt e .csv em uma tabela SQL.
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: cac73bebca185f40deb1b1bac4a77c6ceb20264e
ms.sourcegitcommit: 7035d9471876c70b99c58bf9b46af5cce6e9c66c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2020
ms.locfileid: "87522450"
---
# <a name="sql-server-import-extension-preview"></a>Extensão de Importação do SQL Server (versão prévia)

A extensão de Importação do SQL Server (versão prévia) converte arquivos .txt e .csv em uma tabela SQL. Este assistente utiliza uma estrutura da Microsoft Research conhecida como [PROSE (Program Synthesis using Examples)](https://microsoft.github.io/prose/) para analisar o arquivo de forma inteligente com participação mínima do usuário. Trata-se de uma estrutura avançada para estruturação de dados e conta com a mesma tecnologia que alimenta o Preenchimento Relâmpago no Microsoft Excel

Para saber mais sobre a versão do SSMS desse recurso, você pode ler [este artigo](https://docs.microsoft.com/sql/relational-databases/import-export/import-flat-file-wizard).


## <a name="install-the-sql-server-import-extension"></a>Instalar a extensão de Importação do SQL Server

1. Para abrir o gerenciador de extensões e acessar as extensões disponíveis, selecione o ícone de extensões ou selecione **Extensões** no menu **Exibir**.
2. Selecione uma extensão disponível para exibir os detalhes.

   ![gerenciador da extensão de importação](media/sql-server-import-extension/import-wizard-install.png)

1. Selecione a extensão que você deseja e **Instale**-a.
2. Selecione **Recarregar** para habilitar a extensão (necessário apenas na primeira vez que você instala uma extensão).

## <a name="start-import-wizard"></a>Iniciar Assistente de Importação

1. Para iniciar a Importação do SQL Server, primeiro faça uma conexão com um servidor na guia Servidores.
2. Depois de fazer uma conexão, faça drill down para o banco de dados de destino para o qual deseja importar um arquivo para uma tabela SQL.
3. Clique com o botão direito do mouse no banco de dados e clique em **Assistente de Importação**.
    ![abrir assistente de importação](media/sql-server-import-extension/open-import-wizard.png)

## <a name="importing-a-file"></a>Importando um arquivo
1. Quando você clica com o botão direito do mouse para iniciar o assistente, o servidor e o banco de dados já estão preenchidos automaticamente. Se houver outras conexões ativas, você poderá selecionar na lista suspensa. 
    
    Selecione um arquivo clicando em **Procurar**. Ele deve preencher automaticamente o nome da tabela com base no nome do arquivo, mas você mesmo também pode alterá-lo.

    Por padrão, o esquema será dbo, mas você poderá alterá-lo. Clique em **Avançar** para continuar.
    ![arquivo de entrada](media/sql-server-import-extension/import-wizard-input-file.png)
1. O assistente gerará uma visualização com base nas primeiras 50 linhas. Não há nenhuma ação adicional nesta página além de verificar se os dados parecem precisos. Clique em **Avançar** para continuar.
    ![abrir assistente de importação](media/sql-server-import-extension/import-wizard-preview-data.png)
2. Nesta página, você pode fazer alterações no nome da coluna, no tipo de dados, indicar se é uma chave primária ou permitir nulos. Você pode fazer quantas alterações desejar. Clique em **Importar Dados** para continuar.
    ![abrir assistente de importação](media/sql-server-import-extension/import-wizard-modify-columns.png)
3. Esta página fornece um resumo das ações escolhidas. Você também pode ver se a tabela foi inserida com êxito ou não. 

    Você pode clicar em **Concluído, Anterior** se precisar fazer alterações ou em **Importar novo arquivo** para importar rapidamente outro arquivo.
    ![abrir assistente de importação](media/sql-server-import-extension/import-wizard-summary.png)
1. Verifique se a tabela foi importada com êxito atualizando o banco de dados de destino ou executando uma consulta SELECT no nome da tabela.

## <a name="next-steps"></a>Próximas etapas
- Para obter mais informações sobre o Assistente de Importação, leia a [postagem no blog](https://cloudblogs.microsoft.com/sqlserver/2018/08/30/the-august-release-of-sql-operations-studio-is-now-available/).
- Para saber mais sobre o PROSE, leia a [documentação](https://microsoft.github.io/prose/).
