---
title: Extensão do SQL Server Agent
titleSuffix: Azure Data Studio
description: Instalar e usar a extensão do SQL Server Agent (versão prévia) para o Studio de dados do Azure
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: c21cab43211e168802e8acd94d4664124182b2de
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798052"
---
# <a name="sql-server-agent-extension-preview"></a>Extensão do SQL Server Agent (versão prévia)

A extensão do SQL Server Agent (versão prévia) é uma extensão para gerenciar e solucionar problemas de configuração e os trabalhos do SQL Agent. Essa extensão está atualmente em versão prévia.

As principais ações incluem:
- Trabalhos do agente lista SQL Server configurados em um SQL Server
- Exibir o histórico de trabalhos com os resultados de execução do trabalho
- Controle de trabalho básico para iniciar e parar trabalhos

## <a name="install-the-sql-server-agent-extension"></a>Instalar a extensão do SQL Server Agent

1. Para abrir o Gerenciador de extensões e acessar as **extensões** disponíveis, selecione o ícone de extensões ou selecione extensões no menu **Exibição**.
2. Selecione uma extensão disponível para exibir seus detalhes.

   ![Instalar agente](media/extensions/sql-server-agent-extension/install-sql-agent.png)

1. Selecione a extensão desejada e **instale-a**.
2. Selecione **Recarregar** para habilitar a extensão (necessário somente na primeira vez que você instalar uma extensão).
1. Navegue até o painel de gerenciamento clicando duas vezes o seu servidor ou banco de dados e selecionando **gerenciar**.
2. Extensões instaladas são exibidas como guias no seu painel de gerenciamento:

   ![Agente de modo de exibição](media/extensions/sql-server-agent-extension/view-sql-agent.png)

## <a name="view-jobs"></a>Exibir trabalhos

Quando você se conecta à extensão do SQL Server Agent, a primeira coisa que você vê é uma lista de todos os seus trabalhos de agente.

   ![Exibir trabalhos](media/extensions/sql-server-agent-extension/job-view.png)

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o SQL Server Agent, [verificar nossa documentação.](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent?view=sql-server-2017)


