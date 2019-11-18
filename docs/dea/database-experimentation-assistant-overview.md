---
title: Visão geral do Assistente para Experimentos de Banco de Dados
description: Visão geral do Assistente para Experimentos de Banco de Dados
ms.custom: seo-lt-2019
ms.date: 11/16/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: bb942a7754235fe5e1bc3c72f60ffa1f2f0f61d1
ms.sourcegitcommit: 02b7fa5fa5029068004c0f7cb1abe311855c2254
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2019
ms.locfileid: "74127373"
---
# <a name="overview-of-database-experimentation-assistant"></a>Visão geral do Assistente para Experimentos de Banco de Dados

O Assistente para Experimentos de Banco de Dados (DEA) é uma solução de experimentação para atualizações de SQL Server. O DEA pode ajudá-lo a avaliar uma versão de destino do SQL Server para uma carga de trabalho específica. Os clientes que estão atualizando de versões anteriores do SQL Server (a partir do 2005) para uma versão mais recente do SQL Server podem usar as métricas de análise que a ferramenta fornece.

As métricas de análise de DEA incluem:

- Consultas que têm erros de compatibilidade
- Consultas degradadas e planos de consulta
- Outros dados de comparação de carga de trabalho

Os dados de comparação podem levar a uma maior confiança e uma experiência de atualização bem-sucedida.

## <a name="get-dea"></a>Obter DEA

Para instalar o DEA, [Baixe](https://www.microsoft.com/download/details.aspx?id=54090) a versão mais recente da ferramenta. Em seguida, execute o arquivo **DatabaseExperimentationAssistant. exe** .

## <a name="solution-architecture-for-comparing-workloads"></a>Arquitetura da solução para comparar cargas de trabalho

O diagrama a seguir mostra a arquitetura da solução para uma comparação de carga de trabalho. A comparação de carga de trabalho usa DEA e Distributed Replay durante uma atualização de SQL Server 2008 para SQL Server 2016.

![Arquitetura da solução de comparação de carga de trabalho](./media/database-experimentation-assistant-overview/dea-overview-compare-solution-architecture.png)

## <a name="dea-prerequisites"></a>Pré-requisitos do DEA

A seguir, alguns pré-requisitos para executar o DEA:

- Requisito mínimo de hardware: uma máquina de núcleo único com 3,5 GB de RAM.
- Requisito de hardware ideal: uma CPU de oito núcleos (com 3,5 GB de RAM ou mais). Os processadores com mais de oito núcleos não melhoram os tempos de execução do DEA.
- Um adicional de 33% do tamanho do rastreamento de desempenho é necessário para armazenar os bancos de dados de análise A, B e Report.

## <a name="configure-dea"></a>Configurar o DEA

Na arquitetura de ambiente de pré-requisito, recomendamos que você instale *o DEA no mesmo computador que o controlador de Distributed Replay*. Essa prática evita chamadas entre computadores e simplifica a configuração.

### <a name="required-configuration-for-workload-comparison-using-dea"></a>Configuração necessária para comparação de carga de trabalho usando DEA

DEA conecta-se a servidores de banco de dados usando a autenticação do Windows. Certifique-se de que um usuário que executa o DEA possa se conectar a servidores de banco de dados (origem, destino e análise) usando a autenticação do Windows.

**Requisitos de configuração de captura**

Capturar um rastreamento requer que:

- O usuário que está executando o DEA pode se conectar ao servidor de banco de dados de origem usando a autenticação do Windows.
- O usuário que executa o DEA tem direitos de sysadmin no servidor de banco de dados de origem.
- A conta de serviço que executa o servidor de banco de dados de origem tem acesso de gravação ao caminho da pasta de rastreamento.

Para obter mais informações, consulte perguntas frequentes [sobre a captura de rastreamento](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)

**Requisitos de configuração de reprodução**

Repetir um rastreamento requer que:

- O usuário que está executando o DEA pode se conectar ao servidor de banco de dados de destino usando a autenticação do Windows.
- O usuário que executa o DEA tem direitos sysadmin no servidor de banco de dados de destino.
- A conta de serviço que executa os servidores de banco de dados de destino tem acesso de gravação ao caminho da pasta de rastreamento.
- A conta de serviço que executa Distributed Replay clientes pode se conectar ao servidor de banco de dados de destino usando a autenticação do Windows.
- As portas TCP são abertas para solicitações de entrada no controlador de Distributed Replay. O DEA se comunica com o controlador de Distributed Replay usando interfaces COM.

Para obter mais informações, consulte perguntas frequentes [sobre a reprodução de rastreamento](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)

**Requisitos de configuração de análise**

A execução da análise requer que:

- O usuário que está executando o DEA pode se conectar ao servidor de banco de dados de análise usando a autenticação do Windows.
- O usuário que executa o DEA tem direitos de sysadmin no servidor de banco de dados de origem.

Para obter mais informações, consulte perguntas frequentes [sobre relatórios de análise](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)

## <a name="set-up-telemetry"></a>Configurar telemetria

O DEA tem um recurso habilitado para Internet que pode enviar informações de telemetria à Microsoft para uso no aprimoramento da experiência do produto. As informações coletadas também são salvas no computador para auditoria local, para que você sempre possa ver o que é coletado. Todos os arquivos de log do DEA são salvos na pasta% Temp%\\DEA

Os dados de telemetria podem ser coletados em quatro tipos de eventos:

- **TraceEvent**: eventos de uso para o aplicativo (por exemplo, "disparado parar captura").
- **Exceção**: exceção lançada durante o uso do aplicativo.
- **DiagnosticEvent**: um log de eventos para auxiliar no diagnóstico quando ocorrem problemas (*não* enviados à Microsoft).
- **FeedbackEvent**: comentários do usuário que são enviados por meio do aplicativo.

A coleta e o envio de dados de telemetria são opcionais. Para especificar quais eventos são coletados e se os eventos coletados são enviados à Microsoft, use as seguintes etapas:

1. Vá para o local em que o DEA está instalado (por exemplo, C:\\arquivos de programas (x86)\\Microsoft Corporation\\Assistente para Experimentos de Banco de Dados).
2. Abra e modifique os dois arquivos. config **DEA. exe. config** (para o aplicativo) e **DEACmd. exe. config** (para a CLI) da seguinte maneira:
    - Para interromper a coleta de um tipo de evento, defina o valor de *Event* (por exemplo, **TraceEvent**) como **false**. Para começar a coletar o evento novamente, defina o valor como **true**.
    - Para interromper o salvamento de cópias locais de eventos, defina o valor de **TraceLoggerEnabled** como **false**. Para começar a salvar cópias locais novamente, defina o valor como **true**.
    - Para interromper o envio de eventos à Microsoft, defina o valor de **AppInsightsLoggerEnabled** como **false**. Para começar a enviar eventos para a Microsoft novamente, defina o valor como **true**.

O DEA é regido pela [política de privacidade da Microsoft](https://aka.ms/dea-privacy).

## <a name="next-steps"></a>Próximas etapas

[Introdução](database-experimentation-assistant-get-started.md) orienta as etapas necessárias para capturar, reproduzir e analisar um rastreamento.
