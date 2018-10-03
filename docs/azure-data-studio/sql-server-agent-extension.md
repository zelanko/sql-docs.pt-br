---
title: Extensão de dados Studio SQL Server Agent do Azure | Microsoft Docs
description: Extensão de SQL Server Agent (versão prévia) para o Studio de dados do Azure
ms.custom: tools|sos
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.prod_service: sql-tools
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 5804aa146ddf79f6c3c4ccba48edd86d297c5c72
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "48037827"
---
# <a name="sql-server-agent-extension-preview"></a>Extensão do SQL Server Agent (versão prévia)

A extensão do SQL Server Agent (versão prévia) é uma extensão para gerenciar e solucionar problemas de configuração e os trabalhos do SQL Agent. Esta extensão está atualmente em visualização.

As principais ações incluem:
- Trabalhos do agente lista SQL Server configurados em um SQL Server
- Exibir o histórico de trabalhos com os resultados de execução do trabalho
- Controle de trabalho básico para iniciar e parar trabalhos

## <a name="install-the-sql-server-agent-extension"></a>Instalar a extensão do SQL Server Agent

1. Para abrir o Gerenciador de extensões e acessar as extensões disponíveis, selecione o ícone de extensões ou selecione **extensões** na **exibição** menu.
2. Selecione uma extensão disponível para exibir seus detalhes.

   ![Instalar agente](media/extensions/sql-server-agent-extension/install-sql-agent.png)

1. Selecione a extensão desejada e **instalar** -lo.
2. Selecione **recarregar** para habilitar a extensão (necessário somente na primeira vez que você instalar uma extensão).
1. Navegue até o painel de gerenciamento clicando duas vezes o seu servidor ou banco de dados e selecionando **gerenciar**.
2. Extensões instaladas são exibidas como guias no seu painel de gerenciamento:

   ![Agente de modo de exibição](media/extensions/sql-server-agent-extension/view-sql-agent.png)

## <a name="view-jobs"></a>Exibir trabalhos

Quando você se conecta à extensão do SQL Server Agent, a primeira coisa que você vê é uma lista de todos os seus trabalhos de agente.

   ![Exibir trabalhos](media/extensions/sql-server-agent-extension/job-view.png)

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o SQL Server Agent, [verificar nossa documentação.](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent?view=sql-server-2017)


