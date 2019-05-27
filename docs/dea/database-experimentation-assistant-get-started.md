---
title: Introdução ao Assistente de experimentação do banco de dados para as atualizações do SQL Server
description: Introdução ao Assistente de experimentação do banco de dados
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
ms.openlocfilehash: 45cd72d4383b0bae756b7b8f59502c981dfd6622
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66015133"
---
# <a name="get-started-with-database-experimentation-assistant"></a>Introdução ao Assistente de experimentação do banco de dados

Assistente de experimentação de banco de dados (DEA) é um teste a / B solução para que as alterações em ambientes do SQL Server, como atualizações ou novos índices. DEA ajuda você a avaliar como a carga de trabalho no servidor de origem (em seu ambiente atual) será executado em seu novo ambiente. DEA orienta você por meio da execução de um A / B teste Concluindo três etapas: 

- Capturar
- reprodução
- Análise

Este artigo orienta você através dessas etapas.

## <a name="capture"></a>Capturar

A primeira etapa do SQL Server A / B testes são capturar um rastreamento no servidor de origem. O servidor de origem é geralmente o servidor de produção. Arquivos de rastreamento capturam a carga de trabalho de consulta inteira nesse servidor, incluindo os carimbos de hora. Posteriormente, esse rastreamento é repetido em seus servidores de destino para análise. O relatório de análise fornece informações sobre a diferença no desempenho da carga de trabalho entre os servidores de destino de dois.

Considerações:

- Antes de iniciar a captura de rastreamento, certifique-se de que você faça backup dos bancos de dados do qual você está capturando um rastreamento.
- Um usuário DEA deve ser configurado para se conectar ao banco de dados usando a autenticação do Windows.
- Uma conta de serviço do SQL Server requer acesso ao caminho do arquivo de rastreamento de origem.

Para capturar um rastreamento no servidor de origem:

1. No DEA, acesse **captura todos os** , selecionando o ícone de câmera no menu à esquerda.

   ![Menu de navegação à esquerda](./media/database-experimentation-assistant-get-started/dea-get-started-leftnav.png)

1. Insira ou selecione as seguintes informações:

   - **Nome do rastreamento**: O nome do arquivo para o novo arquivo de rastreamento que você está criando. Evitar um nome de rastreamento que usa a convenção de nomenclatura de arquivo substituição, por exemplo, CaptureName\_NNN.
   - **Duração**: A duração para a captura.
   - **Nome da instância do SQL Server**: A instância do SQL Server do qual você deseja capturar um rastreamento.
   - **Nome do banco de dados**: O nome do banco de dados no computador executando o SQL Server que você deseja capturar um rastreamento do. Se deixado em branco, o rastreamento é capturado de todos os bancos de dados no servidor.
   - **Caminho para armazenar o arquivo de rastreamento de origem no computador SQL Server**: O caminho da pasta onde você deseja salvar o arquivo de rastreamento.

1. Certifique-se de que o banco de dados de destino é feito backup. Em seguida, selecione a caixa de seleção de banco de dados.
1. Selecione **iniciar** para iniciar a captura.

Você pode exibir o progresso de sua captura, incluindo a hora de início, duração e tempo restante. Você também pode iniciar uma nova captura enquanto você aguarda essa captura para concluir. Quando a captura for concluída, use o arquivo de saída de rastreamento para iniciar a segunda fase: reproduzir o arquivo de rastreamento em seus servidores de destino.

Para perguntas comuns sobre a captura de rastreamento, consulte o [capturar as perguntas frequentes sobre](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture).

## <a name="replay"></a>reprodução

A segunda etapa do SQL Server A / B testes são reproduzir o arquivo de rastreamento que foram capturado para os servidores de destino. Em seguida, colete rastreamentos extensivos das repetições para análise. 

Você reproduz o arquivo de rastreamento em dois servidores de destino: um que imita o servidor de origem (destino 1) e outro que simule sua alteração proposta (2 de destino). As configurações de hardware de destino 1 e 2 de destino devem ser o mais semelhantes possível, para que o SQL Server com precisão pode analisar o efeito de desempenho de suas alterações propostas.

Considerações:

- Para executar a reprodução, suas máquinas devem ser definidas para executar rastreamentos Distributed Replay (DReplay). Para obter mais informações, consulte [instalação de controlador e cliente do Distributed Replay](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/).
- Certifique-se de que você restaure os bancos de dados em seus servidores de destino usando o backup do servidor de origem.
- Cache de consulta no SQL Server pode afetar os resultados da avaliação. É recomendável que você reinicie o serviço do SQL Server (MSSQLSERVER) no aplicativo de serviços para aprimorar a consistência nos resultados da avaliação.

Para reproduzir o arquivo de rastreamento:

1. No DEA, selecione o ícone de reprodução no menu à esquerda para ir para **todas as reproduções**. A lista de reprodução dos últimos que são executados durante a sessão, se houver, são exibidos. Para iniciar uma reprodução de novo, selecione **repetir nova**.

1. Insira ou selecione as seguintes informações:

   - **Nome de reprodução**: O nome do arquivo para o rastreamento de reprodução.
   - **O nome de computador do controlador**: O nome do computador do controlador de reprodução distribuída.
   - **Caminho do arquivo de rastreamento de origem no controlador**: O caminho do arquivo para o arquivo de rastreamento do código-fonte da [capturar](#capture).
   - **Nome da instância do SQL Server**: O nome da instância do SQL Server na qual deseja repetir o rastreamento de origem.
   - **Caminho para armazenar o arquivo de rastreamento de destino no computador SQL Server**: O caminho da pasta para o arquivo de rastreamento de repetição resultante.

1. Marque a caixa de seleção para restaurar o backup da primeira etapa.

1. Selecione **iniciar** para iniciar a reprodução. 

Você pode exibir o status da sua reprodução. Depois que você repetir o rastreamento de origem em ambos os servidores de destino, você estará pronto para gerar um relatório de análise.

Para perguntas comuns sobre a reprodução, consulte o [perguntas Frequentes de reprodução](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay).

## <a name="analysis"></a>Análise

A etapa final é gerar um relatório de análise usando reproduzir rastreamentos. O relatório de análise pode ajudá-lo a obter informações sobre as implicações de desempenho da alteração proposta.

Considerações:

- Se um ou mais componentes estiverem ausentes, uma página com links para downloads de pré-requisitos é exibida quando você tenta gerar um novo relatório de análise (conexão de internet necessária).
- Para exibir um relatório que foi gerado em uma versão anterior da ferramenta, você deve primeiro atualizar o esquema.

Para gerar um relatório de análise:

1. No menu à esquerda, acesse **relatórios de análise de**. Conecte-se ao computador executando o SQL Server onde você armazena seus bancos de dados do relatório. É exibida uma lista de todos os relatórios no servidor. Para criar um novo relatório, selecione **novo relatório**.

1. Insira ou selecione as informações necessárias para gerar um relatório:

   - **Nome do relatório**: O nome do relatório de análise para criar.
   - **Rastreamento do SQL Server de destino 1**: O caminho para o arquivo de rastreamento de repetição em 1 de destino.
   - **Rastreamento do SQL Server de destino 2**: O caminho para o arquivo de rastreamento de repetição em 2 de destino.

1. Selecione **iniciar** para gerar o relatório. O novo relatório aparece na parte superior da lista. O ícone ao lado do relatório se torna uma marca de seleção verde quando o relatório foi gerado.

Agora, exiba o relatório de análise para aprofundar fornecida pelo seu A testes a / B.

Para perguntas frequentes sobre relatórios de análise, consulte o [perguntas frequentes sobre análise de](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports).

### <a name="analysis-report"></a>Relatório de análise

Na primeira página do relatório, informações de versão e build para os servidores de destino no qual o teste foi executado são mostradas. Você pode usar o limite para ajustar a confidencialidade ou a tolerância do seu A / análise de teste B. Por padrão, o limite é definido em 5%. Qualquer melhoria no desempenho que é maior ou igual a 5% é categorizada como **aprimorado**. Selecione as opções no menu suspenso para avaliar o relatório usando os limites de desempenho diferentes.

![Limite](https://msdnshared.blob.core.windows.net/media/2017/03/threshold.jpg)

Dois gráficos de pizza demonstram as implicações de desempenho da diferença entre dois servidores alvo para sua carga de trabalho. O gráfico da esquerda é com base na contagem de execução. O gráfico à direita é baseado em consultas distintas. Há cinco categorias possíveis:

- **Aprimorado**:  Estatisticamente, a consulta foi executada melhor em 2 de destino que em 1 de destino.
- **Degradado**: Estatisticamente, a consulta foi executada pior em 2 de destino que em 1 de destino.
- **Mesmo**: Não há nenhuma diferença estatística para a consulta entre 1 de destino e 2 de destino.
- **Não é possível avaliar**: O tamanho da amostra para a consulta é muito pequeno para análise estatística. Para A / B testes análises, DEA requer as mesmas consultas ter pelo menos 30 execuções em cada destino.
- **Erro**: A consulta com erro pelo menos uma vez em um dos destinos.

![Gráfico de pizza](./media/database-experimentation-assistant-get-started/dea-get-started-piechart.png)

Selecione uma fatia para fazer uma busca detalhada em uma categoria específica e obter métricas de desempenho, incluindo o **não é possível avaliar** fatia da pizza.

A página de busca detalhada para um desempenho Alterar categoria mostra uma lista das consultas nessa categoria. O **erro** página possui três guias:

- **Novos erros**: Erros que apareciam em 2 de destino, mas não em 1 de destino.
- **Erros existentes**: Erros que apareciam no destino 1 e 2 de destino.
- **Resolver erros**: Erros que apareciam em 1 de destino, mas não em 2 de destino.

   ![Página de erro](./media/database-experimentation-assistant-get-started/dea-get-started-errorpage.png)

Selecione uma consulta para ir para um **resumo de comparação** página para a consulta.

O **resumo de comparação** página mostra as estatísticas de resumo para a consulta. O resumo inclui o número de execuções, a duração média, média da CPU, média de leituras/gravações e contagem de erros.

![Estatísticas de resumo](./media/database-experimentation-assistant-get-started/dea-get-started-summarystats.png)

Se a consulta é um erro, o **informações de erro** guia mostra mais informações sobre o erro. O **informações de plano de consulta** guia exibe informações sobre os planos de consulta que são usados para a consulta no destino 1 e 2 de destino.

![Plano de consulta](./media/database-experimentation-assistant-get-started/dea-get-started-queryplan.png)

Em qualquer página do relatório de análise, selecione a **imprimir** botão no canto superior direito de imprimir tudo o que é visível.

## <a name="next-steps"></a>Próximas etapas

- Para saber como gerar um arquivo de rastreamento que tem um log de eventos que ocorrem em um servidor, consulte [capturar o rastreamento](database-experimentation-assistant-capture-trace.md).

- Para obter uma introdução 19 minutos DEA e demonstração, assista ao vídeo a seguir:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
