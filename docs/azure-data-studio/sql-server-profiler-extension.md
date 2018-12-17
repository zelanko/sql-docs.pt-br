---
title: Extensão SQL Server Profiler do Azure Data Studio | Microsoft Docs
description: Extensão do SQL Server Profiler (versão prévia) para o Azure Data Studio
ms.custom: tools|sos
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 7f5d1731cfb126b2dbaa259b89b327951d384e1a
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356007"
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

1. Para abrir o Gerenciador de extensões e acessar as extensões disponíveis, selecione o ícone de extensões ou selecione extensões no menu Exibição.
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





