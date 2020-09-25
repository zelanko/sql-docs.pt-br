---
title: Extensão de SQL Server Agent
description: Saiba como instalar e usar a extensão de SQL Server Agent para o Azure Data Studio, uma extensão para gerenciar trabalhos e configurações do SQL Agent.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 3d00919c0967db12dfe678ad541a5a9ed9ecae61
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91122982"
---
# <a name="sql-server-agent-extension-preview"></a>Extensão de SQL Server Agent (versão prévia)

A extensão de SQL Server Agent (versão prévia) é uma extensão para gerenciar e solucionar problemas de trabalhos e configuração do SQL Agent. Esta extensão está em versão prévia.

As principais ações incluem:

- Listar trabalhos do SQL Server Agent configurados em um SQL Server
- Exibir o histórico de trabalhos com os resultados da execução do trabalho
- Controle de trabalho básico para iniciar e parar trabalhos

## <a name="install-the-sql-server-agent-extension"></a>Instalar a extensão de SQL Server Agent

1. Para abrir o gerenciador de extensões e acessar as extensões disponíveis, selecione o ícone de extensões ou selecione **Extensões** no menu **Exibir**.
2. Selecione uma extensão disponível para exibir os detalhes.

   ![Instalar o agente](media/sql-server-agent-extension/install-sql-agent.png)

3. Selecione a extensão que você deseja e **Instale**-a.
4. Selecione **Recarregar** para habilitar a extensão (necessário apenas na primeira vez que você instala uma extensão).
5. Navegue até o painel de gerenciamento clicando com o botão direito do mouse no servidor ou no banco de dados e selecionando **Gerenciar**.
6. As extensões instaladas aparecem como guias no painel de gerenciamento:

   ![Exibir o agente](media/sql-server-agent-extension/view-sql-agent.png)

## <a name="view-jobs"></a>Exibir trabalhos

Quando você se conecta à extensão de SQL Server Agent, a primeira coisa que vê é uma lista de todos os seus trabalhos do Agent.

   ![Exibir trabalhos](media/sql-server-agent-extension/job-view.png)

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o SQL Server Agent, [confira nossa documentação](../../ssms/agent/sql-server-agent.md).
