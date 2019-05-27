---
title: Exibir relatórios de análise no Assistente de experimentação do banco de dados para atualizações do SQL Server
description: Exibir relatórios de análise no Assistente de experimentação do banco de dados
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
manager: craigg
ms.openlocfilehash: 63641dd5b9d9a1e53d68f3be2ae4d5a57cfc1db6
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66015113"
---
# <a name="view-analysis-reports-in-database-experimentation-assistant"></a>Exibir relatórios de análise no Assistente de experimentação do banco de dados

Depois que você [criar seu relatório de análise](database-experimentation-assistant-create-report.md) no banco de dados experimentação Assistant (DEA), conclua as etapas descritas neste artigo para exibir o relatório e obter informações de desempenho fornecidas pelo seu A testes a / B.

## <a name="select-a-server"></a>Selecione um servidor

No DEA, selecione o ícone de menu. No menu expandido, selecione **relatórios de análise de** ao lado do ícone de lista de verificação para abrir a janela de relatórios de análise.

Sob **relatórios de análise de**, insira o nome de um computador executando o SQL Server que tem um banco de dados de análise. Selecione **Conectar**. 

![Conectar-se a um relatório existente](./media/database-experimentation-assistant-view-report/dea-view-report-connect.png)

Se você não tem quaisquer dependências, o **pré-requisitos** página solicita que você com links para instalá-los. Instale os pré-requisitos e, em seguida, selecione **tente novamente**.

![Página pré-requisitos](./media/database-experimentation-assistant-view-report/dea-view-report-prereq.png)

## <a name="select-an-analysis-report-to-view"></a>Selecione para exibir um relatório de análise

Na lista de relatórios de análise, clique duas vezes em um relatório para abri-lo.

![Exibir o relatório existente](./media/database-experimentation-assistant-view-report/dea-view-report-view-existing.png)

Você pode obter percepções sobre quão bem sua carga de trabalho é representada, conforme mostrado neste gráfico de exemplo:

![Gráficos de representante da carga de trabalho](./media/database-experimentation-assistant-view-report/dea-view-report-workload-compare.png)

## <a name="view-and-understand-the-analysis-report"></a>Exibir e compreender o relatório de análise

Esta seção explica o relatório de análise.

### <a name="query-categories"></a>Categorias de consulta

Selecione diferentes fatias do gráfico de pizza à esquerda para mostrar apenas as consultas que se enquadram nessa categoria.

![Relatório fatias da pizza](./media/database-experimentation-assistant-view-report/dea-view-report-pie-slices.png)

- **Degradado consultas**: Consultas que teve um melhor desempenho em r que em B.  
- **Erros**: Consultas que mostram erros na instância B, mas não na instância do r.  
- **Aprimorado de consultas**: Consultas que executou o melhor na instância de B na instância A.  
- **Consultas indeterminadas**: Consultas que tiveram uma alteração de desempenho indeterminado.  
- **Mesmo**: Consultas em que desempenho permaneceu igual entre as instâncias A e B.

### <a name="individual-query-drill-down"></a>Consulta individual drill down

Você pode selecionar os links de modelo de consulta para ver informações mais detalhadas sobre consultas específicas.

![Consulta drill-down](./media/database-experimentation-assistant-view-report/dea-view-report-drilldown.png)

Selecione uma consulta específica para abrir uma comparação de resumida para a consulta.

![Resumo de comparação](./media/database-experimentation-assistant-view-report/dea-view-report-comparison-summary.png)

Você pode ver as instâncias A e B que a consulta foi executada em. Você também pode ver um modelo de como pode ser a consulta. Uma tabela exibe informações de consulta que são específicas para instâncias A e B.

### <a name="error-queries"></a>Consultas de erro

O relatório de resumo de comparação tem expansível **informações de erro** e **informações de plano de consulta** seções. As seções mostram os erros e informações para ambas as instâncias do plano.

Selecione a pizza para mostrar esses tipos de erros de erro (vermelho):
- **Erros existentes**: Erros que estavam em r.
- **Novos erros**: Erros que estavam em B.
- **Resolver erros**: Erros que estavam em um, mas não em B.

![Gráficos de erro](./media/database-experimentation-assistant-view-report/dea-view-report-error-charts.png)

## <a name="next-steps"></a>Próximas etapas

- Para saber como gerar um relatório de análise em um prompt de comando, consulte [executados no prompt de comando](database-experimentation-assistant-run-command-prompt.md).

- Para obter uma introdução 19 minutos DEA e demonstração, assista ao vídeo a seguir:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
