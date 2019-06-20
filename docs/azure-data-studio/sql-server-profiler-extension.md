---
title: Extensão do SQL Server Profiler
titleSuffix: Azure Data Studio
description: Instalar e usar a extensão do SQL Server Profiler (visualização) para o Studio de dados do Azure
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: 92c662a05334731d66891e85e7501e38da438e03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797995"
---
# <a name="sql-server-profiler-extension-preview"></a>Extensão do SQL Server Profiler (versão prévia)

A extensão do SQL Server Profiler (versão prévia) fornece uma solução simples de rastreamento do SQL Server semelhante ao Profiler do SQL Server Management Studio (SSMS), exceto pela criação com os XEvents. O SQL Server Profiler é muito fácil de usar e tem bons valores padrão para as configurações de rastreamento mais comuns. A experiência do usuário é otimizada para a navegação por eventos e para a exibição do texto associado do Transact-SQL (T-SQL). O SQL Server Profiler para o Azure Data Studio também pressupõe bons valores padrão para a coleta de atividades de execução do T-SQL com uma experiência do usuário fácil de usar. Essa extensão está atualmente em versão prévia.

**SQL Profiler-casos de uso comuns:**

- Percorrer consultas problemáticas para localizar a causa do problema.
- Localizar e diagnosticar consultas de execução lenta.
- Capturar a série de instruções Transact-SQL que levam a um problema.
- Monitorar o desempenho do SQL Server para ajustar cargas de trabalho.
- Correlacionar contadores de desempenho para diagnosticar problemas.


## <a name="install-the-sql-server-profiler-extension"></a>Instalar a extensão do SQL Server Profiler

1. Para abrir o Gerenciador de extensões e acessar as **extensões** disponíveis, selecione o ícone de extensões ou selecione extensões no menu **Exibição**.
2. Selecione uma extensão disponível para exibir seus detalhes.

   ![Gerenciador de extensões do criador de perfil](media/extensions/sql-server-profiler-extension/profiler-extension.png)

1. Selecione a extensão desejada e **instale-a**.
2. Selecione **Recarregar** para habilitar a extensão (necessário somente na primeira vez que você instalar uma extensão).

## <a name="start-profiler"></a>Iniciar o Profiler

1. Para iniciar o Profiler, estabeleça uma conexão com um servidor na guia Servidores.
2. Depois de fazer uma conexão, digite **Alt + P** para iniciar o Profiler.
3. Para iniciar o Profiler, pressione **Alt + S.** Agora você pode começar a ver eventos estendidos.
    ![Gerenciador de extensões do criador de perfil](media/extensions/sql-server-profiler-extension/view-profiler.png)    
1. Para parar o Profiler, pressione **Alt + S.** Este atalho alterna entre a execução e pausa do Profiler.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o Profiler e eventos estendidos, consulte [eventos estendidos](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events).





