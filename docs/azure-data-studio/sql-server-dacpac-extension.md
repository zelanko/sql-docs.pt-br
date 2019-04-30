---
title: Extensão de dacpac do SQL Server
titleSuffix: Azure Data Studio
description: Instalar e usar a extensão de dacpac do SQL Server (versão prévia) para o Studio de dados do Azure
ms.custom: seodec18
ms.date: 03/18/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 383a7b2bbd6e8ebaab5f1e66b10a10c9584800ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63309237"
---
# <a name="sql-server-dacpac-extension-preview"></a>Extensão de dacpac do SQL Server (versão prévia)

**A Data-tier Application Wizard** fornece uma experiência fácil de usar para implantar e extrair os arquivos. dacpac e importar e exportar arquivos. bacpac.

Essa experiência está atualmente em visualização inicial. Reportar problemas e solicitações de recursos [aqui.](https://github.com/microsoft/azuredatastudio/issues)

![ações de dados](media/sql-server-dacpac-extension/data-tier-application-actions.png)

 ### <a name="requirements"></a>Requisitos
 * Este assistente requer uma conexão ativa a uma instância do SQL Server para iniciar.

 ### <a name="how-do-i-start-the-data-tier-application-wizard"></a>Como iniciar o Assistente de aplicativo da camada de dados?
 * O ponto de entrada principal para que o assistente é com o botão direito em um banco de dados no Pesquisador de objetos e, em seguida, clique em **Assistente de aplicativo da camada de dados**.
 * Se um usuário estiver conectado a uma instância do SQL Server, o usuário também pode iniciar o assistente na paleta de comandos (Ctrl + Shift + P), pesquisando **Assistente de aplicativo da camada de dados.**

 ### <a name="why-would-i-use-the-data-tier-application-wizard"></a>Por que usar o Assistente de aplicativo da camada de dados?
 Este assistente foi criado para adicionar a capacidade de extrair e implantar arquivos. dacpac e importar e exportar arquivos. bacpac no estúdio de dados do Azure.

## <a name="install-the-sql-server-dacpac-extension"></a>Instalar a extensão de dacpac do SQL Server

1. Para abrir o Gerenciador de extensões e acessar as **extensões** disponíveis, selecione o ícone de extensões ou selecione extensões no menu **Exibição**.
2. Selecione a extensão de dacpac do SQL Server e clique em **instalar**.
1. Selecione **Recarregar** para habilitar a extensão (necessário somente na primeira vez que você instalar uma extensão).
2. Navegue até o painel de gerenciamento clicando duas vezes o seu servidor ou banco de dados e selecionando **gerenciar**.
3. Extensões instaladas são exibidas como guias no seu painel de gerenciamento:

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o dacpac, [verificar nossa documentação.](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017)