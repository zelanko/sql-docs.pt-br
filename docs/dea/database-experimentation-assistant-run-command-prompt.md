---
title: Executar Assistente para Experimentos de Banco de Dados em um prompt de comando
description: Executar Assistente para Experimentos de Banco de Dados em um prompt de comando
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
ms.openlocfilehash: f5a0f7441dd17aec2587c772a678a3681fd3b423
ms.sourcegitcommit: 9e026cfd9f2300f106af929d88a9b43301f5edc2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74317726"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt"></a>Executar Assistente para Experimentos de Banco de Dados em um prompt de comando

Este artigo descreve como capturar um rastreamento no Assistente para Experimentos de Banco de Dados (DEA) e, em seguida, analisar os resultados, tudo a partir de um prompt de comando.

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>Iniciar uma nova captura de carga de trabalho usando o comando DEA

Para iniciar uma nova captura de carga de trabalho, em um prompt de comando, execute o seguinte comando:

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**Exemplo**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload-capture"></a>Reproduzir uma captura de carga de trabalho

1. Faça logon no computador do controlador de Distributed Replay.
2. Para converter o rastreamento de carga de trabalho que você capturou usando o comando DEA para um arquivo IRF, em um prompt de comando, execute o seguinte comando:

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3. Inicie uma captura de rastreamento no computador de destino que executa SQL Server usando StartReplayCaptureTrace. Sql.

    a.  Em SQL Server Management Studio (SSMS), abra <Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.Sql.

    b.  Execute `Set @durationInMins=0` para que a captura de rastreamento não pare automaticamente após uma hora especificada.

    c.  Para definir o tamanho máximo do arquivo por arquivo de rastreamento `Set @maxfilesize`, execute. O tamanho recomendado é 200 (em MB).

    d.  Edite `@Tracefile` para definir um nome exclusivo para o arquivo de rastreamento.

    e.  Edite `@dbname` para especificar um nome de banco de dados se a carga de trabalho deve ser capturada somente em um banco de dados específico. Por padrão, a carga de trabalho em todo o servidor é capturada.

4. Para reproduzir o arquivo IRF em relação à instância de SQL Server de destino, em um prompt de comando, execute o seguinte comando:

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`

    a.  Para monitorar o status, em um prompt de comando, `DReplay status -f 1`execute.

    b.  Para interromper a reprodução, por exemplo, se você observar que a% Pass é menor do que o esperado, em um prompt de `DReplay cancel`comando, execute.

5. Interrompa a captura de rastreamento na instância de SQL Server de destino.
6. No SSMS, abra `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`.
7. Edite `@Tracefile` para corresponder ao caminho do arquivo de rastreamento no computador de destino que executa o SQL Server.
8. Execute o script no computador de destino que executa o SQL Server.

## <a name="analyze-traces-using-the-dea-command"></a>Analisar rastreamentos usando o comando DEA

Para iniciar uma nova análise de rastreamento, em um prompt de comando, execute o seguinte comando:

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**Exemplo**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="see-also"></a>Consulte também

- Para obter mais informações sobre como usar o DEA, consulte [visão geral do assistente para experimentos de banco de dados](database-experimentation-assistant-overview.md).
