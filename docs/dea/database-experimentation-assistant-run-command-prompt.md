---
title: Executar o Assistente de experimentação do banco de dados em um prompt de comando para atualizações do SQL Server
description: Executar o Assistente de experimentação do banco de dados em um prompt de comando
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
manager: jroth
ms.openlocfilehash: c4603bf5fec8f1df8ae1e7fe0e711bf7b6e8f1e9
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794425"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt"></a>Executar o Assistente de experimentação do banco de dados em um prompt de comando

Este artigo descreve como usar a janela de Prompt de comando para capturar um rastreamento no banco de dados experimentação Assistant (DEA) e, em seguida, analise os resultados. 

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>Iniciar uma nova carga de trabalho de captura usando o comando DEA

Para iniciar uma nova captura de carga de trabalho, execute o seguinte comando:

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**Exemplo**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload"></a>Reproduzir uma carga de trabalho

1.  Faça logon no computador do controlador de reprodução distribuída.
2.  Converta o rastreamento de carga de trabalho que você capturou, usando o comando DEA para um arquivo IRF:

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3.  Inicie uma captura de rastreamento no computador de destino executando o SQL Server usando StartReplayCaptureTrace.sql.
       
    a.  No SQL Server Management Studio (SSMS), abra < Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.sql.
    
    b.  Execute `Set @durationInMins=0` para que a captura de rastreamento não para automaticamente após um tempo especificado.
    
    c.  Para definir o tamanho máximo por arquivo de rastreamento, execute `Set @maxfilesize`. O tamanho recomendado é de 200 (em MB).
    
    d.  Editar `@Tracefile` para definir um nome exclusivo para seu arquivo de rastreamento.
    
    e.  Editar `@dbname` para especificar um nome de banco de dados se a carga de trabalho deve ser capturada somente em um banco de dados específico. Por padrão, a carga de trabalho em todo o servidor for capturada. 
4.  Reproduzir o arquivo IRF na instância do SQL Server de destino:

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`
        
    a.  Para monitorar o status, abra uma janela de Prompt de comando e execute `DReplay status -f 1`.
        
    b.  Para interromper a reprodução, tal como se você ver que o % de passagem é menor que o esperado, abra uma janela de Prompt de comando e execute `DReplay cancel`.

5.  Pare a captura de rastreamento na instância do SQL Server de destino.
6.  No SSMS, abra `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`.
7.  Editar `@Tracefile` para corresponder ao caminho do arquivo de rastreamento no computador de destino executando o SQL Server.
8.  Execute o script no computador de destino executando o SQL Server.

## <a name="analyze-traces-by-using-the-dea-command"></a>Analisar rastreamentos usando o comando DEA

Para iniciar uma nova análise do rastreamento, execute o seguinte comando:

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**Exemplo**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="next-steps"></a>Próximas etapas

Para obter uma introdução 19 minutos DEA e demonstração, assista ao vídeo a seguir:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
