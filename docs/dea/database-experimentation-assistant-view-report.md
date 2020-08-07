---
title: Exibir relatórios de análise para atualizações SQL Server
description: Saiba como exibir e entender os relatórios de análise para obter informações de desempenho no Assistente para Experimentos de Banco de Dados (DEA).
ms.custom: seo-lt-2019
ms.date: 02/04/2020
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: pochiraju
ms.author: rajpo
ms.reviewer: mathoma
ms.openlocfilehash: 017b7a1e06fca4a1f682050b99f8c8412b44aaf4
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951121"
---
# <a name="view-analysis-reports-in-database-experimentation-assistant"></a>Exibir relatórios de análise no Assistente para Experimentos de Banco de Dados

Depois de usar Assistente para Experimentos de Banco de Dados (DEA) para [criar um relatório de análise](database-experimentation-assistant-create-report.md), você pode examinar o relatório para obter informações de desempenho com base no teste a/B que você realizou.

## <a name="open-an-existing-analysis-report"></a>Abrir um relatório de análise existente

1. Em DEA, selecione o ícone de lista, especifique o nome do servidor e o tipo de autenticação, marque ou desmarque as caixas de seleção **criptografar conexão** e **certificado do servidor confiável** , conforme apropriado para seu cenário e, em seguida, selecione **conectar**.

   ![Conectar-se ao servidor com o relatório](./media/database-experimentation-assistant-view-report/dea-connect-to-server-with-report-files.png)

2. Na tela **relatórios de análise** , no lado esquerdo, selecione a entrada do relatório que você deseja exibir.

   ![Abrir um arquivo de relatório existente](./media/database-experimentation-assistant-view-report/dea-select-report-to-view.png)

## <a name="view-and-understand-the-analysis-report"></a>Exibir e entender o relatório de análise

Esta seção orienta você pelo relatório de análise.

Na primeira página do relatório, são exibidas informações sobre a versão e as informações de compilação dos servidores de destino nos quais o experimento foi executado. Limite permite que você ajuste a sensibilidade ou a tolerância da sua análise de teste A/B. Por padrão, o limite é definido em 5%; qualquer melhoria no desempenho >= 5% é categorizada como ' aprimorado '.  A lista suspensa permite avaliar o relatório com limites de desempenho diferentes.

Você pode exportar os dados no relatório para um arquivo CSV, selecionando o botão **Exportar** .  Em qualquer página do relatório de análise, você pode selecionar **Imprimir** para imprimir o que está visível na tela naquele momento.

### <a name="query-distribution"></a>Distribuição de consultas

- Selecione fatias diferentes dos gráficos de pizza para mostrar apenas as consultas que pertencem a essa categoria.

   ![Categorias de relatório como fatias de pizza](./media/database-experimentation-assistant-view-report/dea-view-report-pie-slices.png)

  - **Degradado**: consultas que executaram pior no destino 2 do que no destino 1.
  - **Erros**: consultas que mostraram erros pelo menos uma vez em pelo menos um dos destinos.
  - **Aprimorado**: consultas que executaram melhor no destino 2 do que no destino 1.
  - **Não é possível avaliar**: consultas que tinham um tamanho de amostra muito pequeno para análise estatística. Para análise de teste A/B, o DEA exige que as mesmas consultas tenham pelo menos 15 execuções em cada destino.
  - **Mesmo**: consultas que não têm nenhuma diferença estatística entre o destino 1 e o destino 2.

  Consultas de erro, se houver, são mostradas em gráficos separados; um gráfico de barras que classifica erros por tipo e um gráfico de pizza classificando erros por ID de erro.

   ![Gráficos de consulta de erro](./media/database-experimentation-assistant-view-report/dea-error-query-charts.png)

  Há quatro tipos de erros possíveis:

  - **Erros existentes**: erros que existem no destino 1 e no destino 2.
  - **Novos erros**: erros que são novos no destino 2.
  - **Erros resolvidos**: erros que existem no destino 1, mas são resolvidos no destino 2.
  - **Bloqueios de atualização**: erros que bloqueiam a atualização para o servidor de destino.

  Clicar em qualquer seção de barra ou pizza nos gráficos faz uma busca detalhada na categoria e mostra as métricas de desempenho, mesmo para a categoria **não pode avaliar** .

  Além disso, o painel mostra as cinco principais consultas aprimoradas e degradadas para fornecer uma visão geral rápida do desempenho.

### <a name="individual-query-drill-down"></a>Busca detalhada de consulta individual

Você pode selecionar links de modelo de consulta para obter informações mais detalhadas sobre consultas específicas.

![Fazer uma busca detalhada em uma consulta específica](./media/database-experimentation-assistant-view-report/dea-query-drill-down-report.png)

- Selecione uma consulta específica para abrir o resumo de comparação relacionado.

   ![Resumo de comparação](./media/database-experimentation-assistant-view-report/dea-view-report-comparison-summary.png)

   Você pode encontrar estatísticas de resumo para essa consulta, como o número de execuções, duração média, média de CPU, leituras médias/gravações e contagem de erros.  Se a consulta for uma consulta de erro, a guia **informações de erro** mostrará mais detalhes sobre o erro.  Na guia **informações do plano de consulta** , você pode encontrar informações sobre os planos de consulta usados para a consulta nos destinos 1 e 2.

   > [!NOTE]
   > Se você estiver analisando o evento estendido (. XEL) os arquivos, as informações do plano de consulta não são coletadas para limitar a pressão de memória no computador do usuário.

## <a name="see-also"></a>Consulte também

- Para saber como gerar um relatório de análise em um prompt de comando, consulte [executar no prompt de comando](database-experimentation-assistant-run-command-prompt.md).
