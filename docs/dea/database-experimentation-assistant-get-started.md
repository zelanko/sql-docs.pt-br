---
title: Visão geral do processo de comparação de carga de trabalho
description: O Assistente para Experimentos de Banco de Dados (DEA) é uma solução de teste A/B para alterações em ambientes SQL Server, como atualizações ou novos índices.
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: rajsell
ms.reviewer: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 36e36060e16ff85ba2b1fa58d9d900231cf6581f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75258517"
---
# <a name="overview-of-the-workload-comparison-process"></a>Visão geral do processo de comparação de carga de trabalho

Assistente para Experimentos de Banco de Dados (DEA) ajuda a avaliar como a carga de trabalho no seu servidor de origem (em seu ambiente atual) será executada no seu novo ambiente. O DEA orienta você na execução de um teste A/B ao concluir três estágios:

- Capturando um rastreamento de carga de trabalho no servidor de origem.
- Reprodução do rastreamento de carga de trabalho capturado no destino 1 e no destino 2.
- Análise dos rastreamentos de carga de trabalho reproduzidos coletados do destino 1 e destino 2.

Este artigo fornece uma visão geral desse processo.

## <a name="capturing-a-workload-trace"></a>Capturando um rastreamento de carga de trabalho

O primeiro estágio do teste SQL Server A/B é capturar um rastreamento no servidor de origem. O servidor de origem é geralmente o servidor de produção. Os arquivos de rastreamento capturam toda a carga de trabalho de consulta nesse servidor, incluindo carimbos de data/hora.

Considerações:

- Antes de começar, certifique-se de fazer backup dos bancos de dados dos quais você capturará o rastreamento.
- O usuário DEA deve ser capaz de se conectar ao banco de dados usando a autenticação do Windows.
- Uma conta de serviço de SQL Server deve ser capaz de acessar o caminho do arquivo de rastreamento de origem.
- Para DEA determinar se o desempenho de uma consulta foi melhorado ou degradado, essa consulta deve ser executada pelo menos 15 vezes durante o período de captura.

## <a name="replaying-a-workload-trace"></a>Reprodução de um rastreamento de carga de trabalho

O segundo estágio do teste SQL Server A/B é reproduzir o arquivo de rastreamento capturado em dois servidores de destino:

Destino 1, que imita o destino do servidor de origem 2, que imita seu ambiente de destino proposto.

As configurações de hardware do destino 1 e do destino 2 devem ser as mais semelhantes possíveis para que SQL Server possa analisar com precisão o efeito de desempenho de suas alterações propostas.

Considerações:

- Para reproduzir um rastreamento de carga de trabalho, os computadores devem ser configurados para executar rastreamentos Distributed Replay (DReplay).
- Certifique-se de restaurar os bancos de dados nos servidores de destino usando o backup do servidor de origem.
- É recomendável reiniciar o serviço de SQL Server (MSSQLSERVER) no aplicativo de serviços para melhorar a consistência nos resultados da avaliação. O cache de consulta no SQL Server pode afetar os resultados da avaliação.

## <a name="analyzing-the-replayed-workload-traces"></a>Analisando os rastreamentos de carga de trabalho reproduzidos

O estágio final do processo é gerar um relatório de análise usando os rastreamentos de reprodução e revisar o relatório para obter informações sobre as possíveis implicações de desempenho da alteração proposta.

Considerações:

- Se um ou mais componentes estiverem ausentes, uma página pré-requisitos com links para downloads será exibida quando você tentar gerar um novo relatório de análise (conexão com a Internet necessária).
- Para exibir um relatório gerado em uma versão anterior da ferramenta, você deve primeiro atualizar o esquema.

## <a name="see-also"></a>Confira também

- Para saber como produzir um arquivo de rastreamento com um log de eventos que ocorrem em um servidor, consulte o artigo [capturar um rastreamento em Assistente para experimentos de banco de dados](database-experimentation-assistant-capture-trace.md).