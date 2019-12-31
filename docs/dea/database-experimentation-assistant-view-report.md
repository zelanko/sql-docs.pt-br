---
title: Exibir relatórios de análise para atualizações SQL Server
description: Exibir relatórios de análise no Assistente para Experimentos de Banco de Dados
ms.custom: seo-lt-2019
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: b72d49e691311104481637ff49d6c1e09ae0c230
ms.sourcegitcommit: 9e026cfd9f2300f106af929d88a9b43301f5edc2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74317741"
---
# <a name="view-analysis-reports-in-database-experimentation-assistant"></a>Exibir relatórios de análise no Assistente para Experimentos de Banco de Dados

Depois de usar Assistente para Experimentos de Banco de Dados (DEA) para [criar um relatório de análise](database-experimentation-assistant-create-report.md), use as etapas abaixo para examinar o relatório para obter informações de desempenho com base no teste a/B.

## <a name="select-a-server"></a>Selecione um servidor

Em DEA, selecione o ícone de menu. No menu expandido, selecione **relatórios de análise** ao lado do ícone lista de verificação para abrir a janela relatórios de análise.

Em **relatórios de análise**, insira o nome de um computador executando SQL Server que tenha um banco de dados de análise e, em seguida, selecione **conectar**.

![Conectar a um relatório existente](./media/database-experimentation-assistant-view-report/dea-view-report-connect.png)

Se você não tiver nenhuma dependência, a página **pré-requisitos** solicitará os links para instalá-las. Se necessário, instale os pré-requisitos e, em seguida, selecione **tentar novamente**.

![Página pré-requisitos](./media/database-experimentation-assistant-view-report/dea-view-report-prereq.png)

## <a name="select-an-analysis-report-to-view"></a>Selecione um relatório de análise para exibir

Na lista de relatórios de análise, clique duas vezes em um relatório para abri-lo.

![Exibir relatório existente](./media/database-experimentation-assistant-view-report/dea-view-report-view-existing.png)

Você pode obter informações sobre o quão bem sua carga de trabalho é representada, conforme mostrado neste gráfico de exemplo:

![Gráficos do representante de carga de trabalho](./media/database-experimentation-assistant-view-report/dea-view-report-workload-compare.png)

## <a name="view-and-understand-the-analysis-report"></a>Exibir e entender o relatório de análise

Esta seção orienta você pelo relatório de análise.

### <a name="query-categories"></a>Categorias de consulta

Selecione fatias diferentes do gráfico de pizza à esquerda para mostrar apenas as consultas que se enquadram nessa categoria.

![Fatias de pizza de relatório](./media/database-experimentation-assistant-view-report/dea-view-report-pie-slices.png)

- **Consultas degradadas**: consultas que foram executadas melhor em um do que em B.  
- **Erros**: consultas que mostram erros na instância B, mas não na instância A.  
- **Consultas aprimoradas**: consultas que foram executadas melhor na instância B do que na instância A.  
- **Consultas indeterminadas**: consultas que tiveram uma alteração de desempenho indeterminada.  
- **Mesmo**: consultas em que o desempenho permanece o mesmo nas instâncias a e B.

### <a name="individual-query-drill-down"></a>Busca detalhada de consulta individual

Você pode selecionar os links de modelo de consulta para ver informações mais detalhadas sobre consultas específicas.

![Busca detalhada de consulta](./media/database-experimentation-assistant-view-report/dea-view-report-drilldown.png)

Selecione uma consulta específica para abrir um resumo de comparação para a consulta.

![Resumo de comparação](./media/database-experimentation-assistant-view-report/dea-view-report-comparison-summary.png)

Você pode ver as instâncias a e B nas quais a consulta foi executada. Você também pode ver um modelo de como a consulta pode ser. Uma tabela exibe informações de consulta específicas para as instâncias A e B.

### <a name="error-queries"></a>Consultas de erro

O relatório de Resumo de comparação tem **informações de erro** expansíveis e seções de **informações do plano de consulta** . As seções mostram os erros e as informações do plano para ambas as instâncias.

Selecione o erro (vermelho) pizza para mostrar estes tipos de erros:

- **Erros existentes**: erros que estavam em um.
- **Novos erros**: erros que estavam em B.
- **Erros resolvidos**: erros que estavam em um, mas não em B.

![Gráficos de erros](./media/database-experimentation-assistant-view-report/dea-view-report-error-charts.png)

## <a name="see-also"></a>Consulte também

- Para saber como gerar um relatório de análise em um prompt de comando, consulte [executar no prompt de comando](database-experimentation-assistant-run-command-prompt.md).
