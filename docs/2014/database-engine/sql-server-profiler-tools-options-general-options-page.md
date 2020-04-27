---
title: SQL Server Profiler-ferramentas-opções (página Opções Gerais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.tools.generaloptions.f1
helpviewer_keywords:
- General Options dialog box
ms.assetid: a888246d-ccfe-415f-bbdc-d6adafac250a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c9da36f49927acd2a313bcb9f8647655731006d2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089617"
---
# <a name="sql-server-profiler---tools-options-general-options-page"></a>SQL Server Profiler-ferramentas-opções (página Opções Gerais)
  Use a caixa de diálogo **Opções Gerais** para exibir ou especificar as opções a seguir.  
  
## <a name="options"></a>Opções  
  
### <a name="display-options"></a>Opções de Exibição  
 **Nome da fonte**  
 Exibe o nome da fonte usada na grade de resultados de rastreamento durante rastreamentos.  
  
 **Tamanho da fonte**  
 Exibe o tamanho da fonte usada na grade de resultados de rastreamento durante rastreamentos.  
  
 **Escolher Fonte**  
 Abre uma caixa de diálogo para alterar as configurações de fonte.  
  
 **Usar configurações regionais para exibir valores de data e hora**  
 Exibe os valores de data e hora com os parâmetros regionais configurados para seu computador. Se você não selecionar essa opção, os valores de data e hora serão exibidos no formato fixo usado pelo Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]que inclui milissegundos.  
  
> [!NOTE]  
>  Ativar/desativar esta caixa de seleção altera o formato de exibição de colunas de hora como **StartTime** e **EndTime**. Porém, não altera os parâmetros de valores **DateTime** dentro dos eventos de idioma ou RPCs (chamadas de procedimento remoto).  
  
 **Mostrar valores na coluna Duration em microssegundos**  
 Exibe os valores em microssegundos na coluna de dados **Duration** de rastreamentos. Por padrão, a coluna **Duration** exibe valores em milissegundos.  
  
### <a name="tracing-options"></a>Opções de Rastreamento  
 **Iniciar rastreamento imediatamente após estabelecer a conexão.**  
 Começa a rastrear usando o modelo padrão assim que uma conexão é estabelecida.  
  
 **Atualizar a definição de rastreamento quando a versão do provedor for alterada**  
 Aplica a definição de rastreamento mais recente ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] quando o provedor for atualizado. Este item não é verificado por padrão. Isso força o [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] a consultar o servidor quanto à definição de rastreamento e a recriar o arquivo em disco, se houver um.  
  
### <a name="file-rollover-options"></a>Opções de substituição de arquivos  
 **Carregar todos os arquivos de substituição em sequência, sem avisar**  
 Carrega automaticamente os arquivos de substituição quando um arquivo de rastreamento é aberto. Se mais de um arquivo foi criado durante o rastreamento, selecionar esta opção carregará automaticamente todos os arquivos de substituição.  
  
 **Perguntar antes de carregar arquivos de substituição**  
 O [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] pergunta antes de adicionar um arquivo de substituição quando um arquivo de rastreamento é aberto.  
  
 **Nunca carregar arquivos de substituição subsequentes**  
 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] nunca carrega arquivos de substituição posteriores quando um arquivo de rastreamento é aberto.  
  
### <a name="replay-options"></a>Opções de Repetição  
 **Número padrão de threads de repetição**  
 Especifica o número de threads de repetição a usar simultaneamente. Um número mais alto consome mais recursos durante a repetição, porém aumenta a simultaneidade da repetição.  
  
 **Intervalo de espera padrão do monitor de integridade (s)**  
 Especifica o intervalo de espera de repetição, em segundos. O padrão é 3600 segundos (1 hora). Esta configuração afeta o tempo durante o qual um thread pode ser executado antes de ser concluído pelo monitor de integridade.  
  
 **Intervalo de sondagem padrão do monitor de integridade (s)**  
 Especifica o intervalo de sondagem do monitor de integridade durante a repetição, em segundos. O padrão é 60 segundos. Este valor permite que o usuário configure com que frequência o monitor de integridade sonda candidatos a conclusão.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar um rastreamento automaticamente após a conexão com um servidor &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)   
 [Definir padrões de exibição de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)   
 [Reproduzir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [Reproduzir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [Reproduzir rastreamentos](../tools/sql-server-profiler/replay-traces.md)   
 [Definir opções de rastreamento global &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/set-global-trace-options-sql-server-profiler.md)   
 [Modelos e permissões de SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
