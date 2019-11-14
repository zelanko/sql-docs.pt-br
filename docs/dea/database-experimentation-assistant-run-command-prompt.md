---
title: Executar Assistente para Experimentos de Banco de Dados em um prompt de comando
description: Executar Assistente para Experimentos de Banco de Dados em um prompt de comando
ms.custom: seo-lt-2019
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
ms.openlocfilehash: c3b87eafa460cfef69666a3837f56626dab81d47
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056569"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt-sql-server"></a>Executar Assistente para Experimentos de Banco de Dados em um prompt de comando (SQL Server)

Este artigo descreve como usar a janela de prompt de comando para capturar um rastreamento no Assistente para Experimentos de Banco de Dados (DEA) e, em seguida, analisar os resultados. 

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>Iniciar uma nova captura de carga de trabalho usando o comando DEA

Para iniciar uma nova captura de carga de trabalho, execute o seguinte comando:

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**Exemplo**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload"></a>Reproduzir uma carga de trabalho

1.  Faça logon no computador do controlador de Distributed Replay.
2.  Converta o rastreamento de carga de trabalho que você capturou usando o comando DEA para um arquivo IRF:

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3.  Inicie uma captura de rastreamento no computador de destino que executa o SQL Server usando StartReplayCaptureTrace. Sql.
       
    A.  No SQL Server Management Studio (SSMS), abra < Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.sql.
    
    b.  Execute `Set @durationInMins=0` para que a captura de rastreamento não pare automaticamente após uma hora especificada.
    
    c.  Para definir o tamanho máximo do arquivo por arquivo de rastreamento, execute `Set @maxfilesize`. O tamanho recomendado é 200 (em MB).
    
    d.  Edite `@Tracefile` para definir um nome exclusivo para o arquivo de rastreamento.
    
    e.  Edite `@dbname` para especificar um nome de banco de dados se a carga de trabalho deve ser capturada somente em um banco de dados específico. Por padrão, a carga de trabalho em todo o servidor é capturada. 
4.  Reproduza o arquivo IRF em relação à instância de SQL Server de destino:

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`
        
    A.  Para monitorar o status, abra uma janela de prompt de comando e execute `DReplay status -f 1`.
        
    b.  Para interromper a reprodução, como se você observar que a% Pass é menor do que o esperado, abra uma janela de prompt de comando e execute `DReplay cancel`.

5.  Interrompa a captura de rastreamento na instância de SQL Server de destino.
6.  No SSMS, abra `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`.
7.  Edite `@Tracefile` para corresponder ao caminho do arquivo de rastreamento no computador de destino que está executando SQL Server.
8.  Execute o script no computador de destino que executa o SQL Server.

## <a name="analyze-traces-by-using-the-dea-command"></a>Analisar rastreamentos usando o comando DEA

Para iniciar uma nova análise de rastreamento, execute o seguinte comando:

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**Exemplo**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="next-steps"></a>Próximas etapas

Para uma introdução de 19 minutos ao DEA e à demonstração, Assista ao vídeo a seguir:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
