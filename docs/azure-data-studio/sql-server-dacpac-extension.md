---
title: Extensão dacpac do SQL Server
titleSuffix: Azure Data Studio
description: Instale e use a extensão dacpac do SQL Server (versão prévia) para o Azure Data Studio
ms.custom: seodec18
ms.date: 03/18/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: e40e377310b33034b4abecdc5e58eab17d39695d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959193"
---
# <a name="sql-server-dacpac-extension-preview"></a>Extensão de dacpac do SQL Server (versão prévia)

O **Assistente de Aplicativo da Camada de Dados** proporciona uma experiência fácil de usar para implantar e extrair arquivos .dacpac e importar e exportar arquivos .bacpac.

Atualmente, essa experiência está na versão prévia inicial. Informe sobre problemas e solicite recursos [aqui](https://github.com/microsoft/azuredatastudio/issues).

![ações de dados](media/sql-server-dacpac-extension/data-tier-application-actions.png)

 ### <a name="requirements"></a>Requisitos
 * Este assistente requer uma conexão ativa com uma instância do SQL Server para ser iniciado.

 ### <a name="how-do-i-start-the-data-tier-application-wizard"></a>Como fazer para iniciar o assistente do Aplicativo da Camada de Dados?
 * O ponto de entrada principal do assistente é clicar com o botão direito do mouse em um banco de dados no Pesquisador de Objetos e clicar em **Assistente de Aplicativo da Camada de Dados**.
 * Se um usuário estiver conectado a uma instância do SQL Server, ele também poderá iniciar o assistente na paleta de comandos (Ctrl + Shift + P) pesquisando por **Assistente de Aplicativo da Camada de Dados**.

 ### <a name="why-would-i-use-the-data-tier-application-wizard"></a>Por que usar o assistente do Aplicativo da Camada de Dados?
 Este assistente foi criado para adicionar a capacidade de extrair e implantar arquivos .dacpac e importar e exportar arquivos .bacpac no Azure Data Studio.

## <a name="install-the-sql-server-dacpac-extension"></a>Instalar a extensão dacpac do SQL Server adicionada

1. Para abrir o gerenciador de extensões e acessar as extensões disponíveis, selecione o ícone de extensões ou selecione **Extensões** no menu **Exibir**.
2. Selecione a extensão dacpac do SQL Server e clique em **Instalar**.
1. Selecione **Recarregar** para habilitar a extensão (necessário apenas na primeira vez que você instala uma extensão).
2. Navegue até o painel de gerenciamento clicando com o botão direito do mouse no servidor ou no banco de dados e selecionando **Gerenciar**.
3. As extensões instaladas aparecem como guias no painel de gerenciamento:

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre dacpacs, [confira nossa documentação](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017).