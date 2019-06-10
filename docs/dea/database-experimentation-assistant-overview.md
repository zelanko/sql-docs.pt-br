---
title: Visão geral da solução o Assistente de experimentação do banco de dados para o SQL Server é atualizado
description: Visão geral do Assistente para experimentos de banco de dados
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
manager: jroth
ms.openlocfilehash: 25b5d051f6241919f34a60a42582e8a101052290
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794454"
---
# <a name="overview-of-database-experimentation-assistant"></a>Visão geral do Assistente para experimentos de banco de dados

Assistente de experimentação de banco de dados (DEA) é uma solução de experimentação para atualizações do SQL Server. DEA pode ajudá-lo a avaliar uma versão de destino do SQL Server para uma carga de trabalho específica. Os clientes que estão atualizando de versões anteriores do SQL Server (começando com o 2005) para uma versão mais recente do SQL Server podem usar as métricas de análise que fornece a ferramenta. 

As métricas de análise DEA incluem:
- Consultas que têm erros de compatibilidade
- Degradação de consultas e planos de consulta
- Outros dados de comparação de carga de trabalho

Dados de comparação podem resultar em maior confiança e uma experiência de atualização bem-sucedida.

Para obter uma introdução 19 minutos DEA e uma demonstração, assista ao vídeo a seguir:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]

## <a name="get-dea"></a>Obter DEA

Para instalar DEA, [baixar](https://www.microsoft.com/download/details.aspx?id=54090) a versão mais recente da ferramenta. Em seguida, execute as **DatabaseExperimentationAssistant.exe** arquivo.

## <a name="solution-architecture-for-comparing-workloads"></a>Arquitetura da solução para comparar as cargas de trabalho

O diagrama a seguir mostra a arquitetura da solução para obter uma comparação de carga de trabalho. A comparação de carga de trabalho usa DEA e Distributed Replay durante uma atualização do SQL Server 2008 para o SQL Server 2016.

![Arquitetura de solução de comparação de carga de trabalho](./media/database-experimentation-assistant-overview/dea-overview-compare-solution-architecture.png)

## <a name="dea-prerequisites"></a>Pré-requisitos DEA

A seguir estão alguns pré-requisitos para a execução DEA:
- Requisitos mínimos de hardware: Uma máquina de núcleo único com 3,5 GB de RAM.
- Requisito de hardware ideal: Uma CPU de oito núcleos (com 3,5 GB de RAM ou mais). Processadores que têm mais de oito núcleos não melhorar DEA tempos de execução.
- Um adicional 33% do tamanho do rastreamento de desempenho é necessário para a loja A, B e bancos de dados de análise de relatório.

## <a name="configure-dea"></a>Configurar DEA

A arquitetura do ambiente de pré-requisitos, é recomendável que você instale DEA *no mesmo computador que o controlador do Distributed Replay*. Essa prática evita chamadas entre computadores e simplifica a configuração.

### <a name="required-configuration-for-workload-comparison-by-using-dea"></a>Configuração necessária para comparação de carga de trabalho usando DEA

DEA conecta-se aos servidores de banco de dados usando a autenticação do Windows. Certifique-se de que um usuário executar DEA pode se conectar aos servidores de banco de dados (origem, destino e análise) por meio da autenticação do Windows.

**Requisitos de configuração de captura**:

*   Usuário que está executando DEA pode se conectar ao servidor de banco de dados de origem usando a autenticação do Windows.
*   Usuário que está executando DEA tem direitos de sysadmin no servidor de banco de dados de origem.
*   Conta de serviço que executa o servidor de banco de dados de origem tem acesso de gravação ao caminho da pasta de rastreamento.

Para obter mais informações, consulte o [capturar as perguntas Frequentes](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)

**Requisitos de configuração de reprodução**: 

*   Usuário que está executando DEA pode se conectar ao servidor de banco de dados de destino usando a autenticação do Windows.
*   Usuário que está executando DEA tem direitos de sysadmin no servidor de banco de dados de destino.
*   Conta de serviço executando servidores de banco de dados de destino tem acesso de gravação ao caminho da pasta de rastreamento.
*   Conta de serviço que está executando a clientes do Distributed Replay pode se conectar ao servidor de banco de dados de destino usando a autenticação do Windows.
*   DEA se comunica com o controlador do Distributed Replay por meio de interfaces COM. Certifique-se de que as portas TCP estejam abertas para solicitações de entrada no controlador do Distributed Replay.

Para obter mais informações, consulte o [perguntas Frequentes de reprodução](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)

**Requisitos de configuração de análise**: 

*   Usuário que está executando DEA pode se conectar ao servidor de banco de dados de análise usando a autenticação do Windows.
*   Usuário que está executando DEA tem direitos de sysadmin no servidor de banco de dados de origem.

Para obter mais informações, consulte o [análise perguntas Frequentes](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)

## <a name="set-up-telemetry"></a>Configurar a Telemetria

DEA tem um recurso habilitados para internet que pode enviar informações de telemetria à Microsoft. A Microsoft coleta a telemetria para aprimorar a experiência de produto. A telemetria é opcional. As informações coletadas também é salvo no seu computador para a auditoria local. Você sempre pode ver o que é coletado. Todos os arquivos de log de DEA são salvos na pasta % temp %\\pasta DEA.

Você pode decidir quais eventos são coletados. Você também pode decidir se os eventos coletados são enviados à Microsoft. Há quatro tipos de eventos:

*   **TraceEvent**: Eventos de uso para o aplicativo (por exemplo, "disparado parar a captura").
*   **Exceção**: Exceção lançada durante o uso do aplicativo.
*   **DiagnosticEvent**: Um log de eventos para ajudá-lo com o diagnóstico quando ocorrem problemas (*não* enviados à Microsoft).
*   **FeedbackEvent**: Comentários do usuário que é enviado por meio do aplicativo.

Estas etapas mostram como escolher quais eventos são coletados e se os eventos são enviados à Microsoft:

1.  Vá para o local onde DEA está instalado (por exemplo, c:\\arquivos de programas (x86)\\Microsoft Corporation\\Assistente de experimentação do banco de dados).
2.  Abra os dois arquivos. config: DEA.exe.config (para o aplicativo) e DEACmd.exe.config (para a CLI).
3.  Para interromper a coleta de um tipo de evento, defina o valor da *evento* (por exemplo, **TraceEvent**) para **false**. Para começar a coletar o evento novamente, defina o valor como **verdadeira**.
4.  Para parar de salvar cópias locais dos eventos, defina o valor da **TraceLoggerEnabled** à **falso**. Para começar a salvar cópias locais novamente, defina o valor como **verdadeira**.
5.  Para interromper o envio de eventos para a Microsoft, defina o valor da **AppInsightsLoggerEnabled** à **falso**. Para começar a enviar eventos para a Microsoft novamente, defina o valor como **verdadeira**.

DEA é regido pela [declaração de privacidade do Microsoft](https://aka.ms/dea-privacy).

## <a name="next-steps"></a>Próximas etapas

[Introdução ao](database-experimentation-assistant-get-started.md) orienta você pelas etapas necessárias para capturar, repetir e analisar um rastreamento.
