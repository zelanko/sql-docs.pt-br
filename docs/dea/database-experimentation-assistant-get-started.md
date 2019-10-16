---
title: Introdução ao Assistente para Experimentos de Banco de Dados para atualizações de SQL Server
description: Introdução ao Assistente para Experimentos de Banco de Dados
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
ms.openlocfilehash: 9fe162b2a9bc0db4a2a49648eecb76c5802f57c0
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381770"
---
# <a name="get-started-with-database-experimentation-assistant"></a>Introdução ao Assistente para Experimentos de Banco de Dados

O Assistente para Experimentos de Banco de Dados (DEA) é uma solução de teste A/B para alterações em ambientes SQL Server, como atualizações ou novos índices. O DEA ajuda a avaliar como a carga de trabalho no servidor de origem (no seu ambiente atual) será executada no seu novo ambiente. O DEA orienta você na execução de um teste A/B ao concluir três etapas: 

- Capturar
- Reprodução
- Análise

Este artigo orienta você durante essas etapas.

## <a name="capture"></a>Capturar

A primeira etapa de SQL Server teste A/B é capturar um rastreamento no servidor de origem. O servidor de origem geralmente é o servidor de produção. Os arquivos de rastreamento capturam toda a carga de trabalho de consulta nesse servidor, incluindo carimbos de data/hora. Posteriormente, esse rastreamento é reproduzido nos servidores de destino para análise. O relatório de análise fornece informações sobre a diferença no desempenho da carga de trabalho entre os dois servidores de destino.

Considerações:

- Antes de iniciar a captura de rastreamento, certifique-se de fazer backup dos bancos de dados dos quais você está capturando um rastreamento.
- Um usuário do DEA deve ser configurado para se conectar ao banco de dados usando a autenticação do Windows.
- Uma conta de serviço SQL Server requer acesso ao caminho do arquivo de rastreamento de origem.
- Para DEA determinar se o desempenho de uma consulta foi melhorado ou degradado, essa consulta deve ser executada pelo menos 15 vezes durante o período de captura.  

Para capturar um rastreamento no servidor de origem:

1. No DEA, vá para **todas as capturas** selecionando o ícone de câmera no menu à esquerda.

   ![Menu de navegação à esquerda](./media/database-experimentation-assistant-get-started/dea-get-started-leftnav.png)

1. Insira ou selecione as seguintes informações:

   - **Nome do rastreamento**: o nome de arquivo para o novo arquivo de rastreamento que você está criando. Evite um nome de rastreamento que usa a Convenção de nomenclatura de arquivo de substituição, por exemplo, Capturename @ no__t-0NNN.
   - **Duração**: a duração da captura.
   - **Nome da instância de SQL Server**: a instância de SQL Server da qual você deseja capturar um rastreamento.
   - **Nome do banco de dados**: o nome do banco de dados no computador que executa SQL Server que você deseja capturar um rastreamento. Se for deixado em branco, o rastreamento será capturado de todos os bancos de dados no servidor.
   - **Caminho para armazenar o arquivo de rastreamento de origem no computador SQL Server**: o caminho da pasta onde você deseja salvar o arquivo de rastreamento.

1. Verifique se o backup do banco de dados de destino é feito. Em seguida, marque a caixa de seleção banco de dados.
1. Selecione **Iniciar** para iniciar a captura.

Você pode exibir o progresso de sua captura, incluindo hora de início, duração e tempo restante. Você também pode iniciar uma nova captura enquanto aguarda a conclusão dessa captura. Quando a captura for concluída, use o arquivo de rastreamento de saída para iniciar a segunda fase: reproduzir o arquivo de rastreamento nos servidores de destino.

Para perguntas comuns sobre a captura de rastreamento, consulte as [perguntas frequentes sobre captura](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture).

## <a name="replay"></a>Reprodução

A segunda etapa de SQL Server teste a/B é reproduzir o arquivo de rastreamento que foi capturado para seus servidores de destino. Em seguida, colete rastreamentos extensos das repetições para análise. 

Você repete o arquivo de rastreamento em dois servidores de destino: um que imita seu servidor de origem (destino 1) e outro que imita a alteração proposta (destino 2). As configurações de hardware do destino 1 e do destino 2 devem ser as mais semelhantes possíveis, portanto SQL Server pode analisar com precisão o efeito de desempenho de suas alterações propostas.

Considerações:

- Para executar a reprodução, os computadores devem ser configurados para executar rastreamentos Distributed Replay (DReplay). Para obter mais informações, consulte [Distributed Replay controlador e instalação do cliente](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/).
- Certifique-se de restaurar os bancos de dados nos servidores de destino usando o backup do servidor de origem.
- O cache de consulta no SQL Server pode afetar os resultados da avaliação. Recomendamos que você reinicie o serviço de SQL Server (MSSQLSERVER) no aplicativo de serviços para melhorar a consistência nos resultados da avaliação.

Para repetir o arquivo de rastreamento:

1. Em DEA, selecione o ícone reproduzir no menu à esquerda para ir para **todas as repetições**. A lista de repetições passadas que são executadas durante a sessão, se houver, aparece. Para iniciar uma nova reprodução, selecione **nova reprodução**.

1. Insira ou selecione as seguintes informações:

   - **Nome de reprodução**: o nome do arquivo para o rastreamento de reprodução.
   - **Nome do computador do controlador**: o nome do computador do controlador de Distributed Replay.
   - **Caminho para o arquivo de rastreamento de origem no controlador**: o caminho de arquivo do arquivo de rastreamento de origem da [captura](#capture).
   - **Nome da instância de SQL Server**: o nome da instância de SQL Server na qual reproduzir o rastreamento de origem.
   - **Caminho para armazenar o arquivo de rastreamento de destino no computador SQL Server**: o caminho da pasta para o arquivo de rastreamento de reprodução resultante.

1. Marque a caixa de seleção para restaurar o backup da primeira etapa.

1. Selecione **Iniciar** para iniciar a reprodução. 

Você pode exibir o status de sua reprodução. Depois de reproduzir o rastreamento de origem em ambos os servidores de destino, você estará pronto para gerar um relatório de análise.

Para perguntas comuns sobre reprodução, consulte as [perguntas frequentes sobre reprodução](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay).

## <a name="analysis"></a>Análise

A etapa final é gerar um relatório de análise usando os rastreamentos de reprodução. O relatório de análise pode ajudá-lo a obter informações sobre as implicações de desempenho da alteração proposta.

Considerações:

- Se um ou mais componentes estiverem ausentes, uma página pré-requisitos com links para downloads será exibida quando você tentar gerar um novo relatório de análise (conexão com a Internet necessária).
- Para exibir um relatório que foi gerado em uma versão anterior da ferramenta, você deve primeiro atualizar o esquema.

Para gerar um relatório de análise:

1. No menu à esquerda, vá para **relatórios de análise**. Conecte-se ao computador que executa SQL Server em que você armazena seus bancos de dados de relatório. Uma lista de todos os relatórios no servidor é exibida. Para criar um novo relatório, selecione **novo relatório**.

1. Insira ou selecione as informações necessárias para gerar um relatório:

   - **Nome do relatório**: o nome do relatório de análise a ser criado.
   - **Rastreamento para o destino 1 SQL Server**: o caminho para o arquivo de rastreamento reproduzir no destino 1.
   - **Rastreamento para destino 2 SQL Server**: o caminho para o arquivo de rastreamento reproduzir no destino 2.

1. Selecione **Iniciar** para gerar o relatório. O novo relatório é exibido na parte superior da lista. O ícone ao lado do relatório se torna uma marca de seleção verde quando o relatório é gerado.

Agora, exiba o relatório de análise para obter informações fornecidas pelo seu teste A/B.

Para perguntas comuns sobre relatórios de análise, consulte as [perguntas frequentes sobre análise](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports).

### <a name="analysis-report"></a>Relatório de análise

Na primeira página do relatório, a versão e as informações de compilação dos servidores de destino nos quais o experimento foi executado são mostradas. Você pode usar o limite para ajustar a sensibilidade ou a tolerância da sua análise de teste A/B. Por padrão, o limite é definido em 5%. Qualquer melhoria no desempenho que seja maior ou igual a 5% é categorizada como **aprimorada**. Selecione opções no menu suspenso para avaliar o relatório usando diferentes limites de desempenho.

![Limite](https://msdnshared.blob.core.windows.net/media/2017/03/threshold.jpg)

Dois gráficos de pizza demonstram as implicações de desempenho da diferença entre os dois servidores de destino para sua carga de trabalho. O gráfico esquerdo é baseado na contagem de execução. O gráfico correto se baseia em consultas distintas. Há cinco categorias possíveis:

- **Aprimorado**: estatisticamente, a consulta foi melhorada no destino 2 do que no destino 1.
- **Degradado**: estatisticamente, a consulta ficou pior no destino 2 do que no destino 1.
- **Mesmo**: não há nenhuma diferença estatística para a consulta entre o destino 1 e o destino 2.
- **Não é possível avaliar**: o tamanho da amostra da consulta é muito pequeno para análise estatística. Para análise de teste A/B, o DEA exige que as mesmas consultas tenham pelo menos 30 execuções em cada destino.
- **Erro**: a consulta foi disparada pelo menos uma vez em um dos destinos.

![Gráfico de pizza](./media/database-experimentation-assistant-get-started/dea-get-started-piechart.png)

Selecione uma fatia para fazer uma busca detalhada em uma categoria específica e obter métricas de desempenho, incluindo a fatia de pizza **não pode ser avaliada** .

A página de busca detalhada para uma categoria de alteração de desempenho mostra uma lista de consultas nessa categoria. A página de **erro** tem três guias:

- **Novos erros**: erros que apareciam no destino 2, mas não no destino 1.
- **Erros existentes**: erros que apareciam no destino 1 e no destino 2.
- **Erros resolvidos**: erros que apareciam no destino 1, mas não no destino 2.

   ![Página de erro](./media/database-experimentation-assistant-get-started/dea-get-started-errorpage.png)

Selecione uma consulta para ir para uma página de **Resumo de comparação** para essa consulta.

A página **Resumo de comparação** mostra as estatísticas de resumo para essa consulta. O resumo inclui o número de execuções, a duração média, a média da CPU, leituras médias/gravações e a contagem de erros.

![Estatísticas de resumo](./media/database-experimentation-assistant-get-started/dea-get-started-summarystats.png)

Se a consulta for uma consulta de erro, a guia **informações de erro** mostrará mais informações sobre o erro. A guia **informações do plano de consulta** mostra informações sobre os planos de consulta que são usados para a consulta nos destinos 1 e 2.

![Plano de consulta](./media/database-experimentation-assistant-get-started/dea-get-started-queryplan.png)

Em qualquer página do relatório de análise, selecione o botão **Imprimir** no canto superior direito para imprimir tudo que está visível.

## <a name="next-steps"></a>Próximas etapas

- Para saber como produzir um arquivo de rastreamento que tenha um log de eventos que ocorrem em um servidor, consulte [capturar rastreamento](database-experimentation-assistant-capture-trace.md).

- Para uma introdução de 19 minutos ao DEA e à demonstração, Assista ao vídeo a seguir:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
