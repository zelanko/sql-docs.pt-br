---
title: Executar Assistente para Experimentos de Banco de Dados em um prompt de comando
description: Executar Assistente para Experimentos de Banco de Dados em um prompt de comando
ms.custom: seo-lt-2019
ms.date: 02/25/2020
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: 674f40b16437547956178293c5b491b11c8b2f89
ms.sourcegitcommit: d973b520f387b568edf1d637ae37d117e1d4ce32
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85215483"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt"></a>Executar Assistente para Experimentos de Banco de Dados em um prompt de comando

Este artigo descreve como capturar um rastreamento no Assistente para Experimentos de Banco de Dados (DEA) e, em seguida, analisar os resultados, tudo a partir de um prompt de comando.

   > [!NOTE]
   > Para saber mais sobre cada operação DEA, tente executar o seguinte comando:
   >
   > `Deacmd.exe -o <operation> --help`
   >
   > Um nome de operação é necessário; as operações válidas são **Analysis**, **StartCapture**e **StopCapture**.

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>Iniciar uma nova captura de carga de trabalho usando o comando DEA

Para iniciar uma nova captura de carga de trabalho, em um prompt de comando, execute o seguinte comando:

`Deacmd.exe -o StartCapture -n <Trace FileName> -x <Trace Format> -h <SQLServerInstance> -f <database name> -e <Encrypt Connection> -m <Authetication Mode> -u <user name> -p <password> -l <Location of Output Folder> -d <duration>`

**Exemplo**

`Deacmd.exe -o StartCapture -n sql2008capture -x 0 -h localhost -f adventureworks -e --trust -m 0 -l c:\test  -d 60`

**Opções adicionais**

Ao iniciar uma nova captura de carga de trabalho com o `Deacmd.exe` comando, você pode usar as seguintes opções adicionais:

| Opção| Descrição |  
| --- | --- |
| -n, --name | Necessária nome do arquivo de rastreamento |
| -x,--formato | Necessária formato do rastreamento (Trace = 0, XEvents = 1) |
| -d,--duração | Necessária duração máxima da captura, em minutos |
| -l, --location | Necessária local da pasta de saída para armazenar arquivos de rastreamento/XEvent no computador host |
| -t,--tipo | (Padrão: 0) tipo/edição do SQL Server (SqlServer = 0, AzureSQLDB = 1, Azure SQL Instância Gerenciada = 2) |
| -h,--host | Necessária SQL Server nome do host e/ou nome da instância para iniciar a captura |
| -e,--criptografar | (Padrão: true) Criptografar conexão com SQL Server instância. O padrão é verdadeiro |
| --confiar | (Padrão: false) Confiar no certificado do servidor ao conectar-se à instância do SQL Server. O padrão é falso |
| -f,--DatabaseName | (Padrão:) Nome do banco de dados para filtrar os rastreamentos, se não especificado, a captura será iniciada em todos os bancos de dados |
| -m,--AuthMode | (Padrão: 0) modo de autenticação (Windows = 0, autenticação do SQL = 1) |
| -u,--nome de usuário | Nome de usuário para se conectar ao SQL Server |
| -p,--senha | Senha para se conectar ao SQL Server |

## <a name="replay-a-workload-capture"></a>Reproduzir uma captura de carga de trabalho

**Usando Distributed Replay**

Se você estiver usando Distributed Replay, execute as etapas a seguir.

1. Faça logon no computador do controlador de Distributed Replay.
2. Para converter o rastreamento de carga de trabalho que você capturou usando o comando DEA para um arquivo IRF, em um prompt de comando, execute o seguinte comando:

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3. Inicie uma captura de rastreamento no computador de destino que executa SQL Server usando StartReplayCaptureTrace. Sql.

    a.  Em SQL Server Management Studio (SSMS), abra <Dea_InstallPath \> \Scripts\StartReplayCaptureTrace.Sql.

    b.  Execute `Set @durationInMins=0` para que a captura de rastreamento não pare automaticamente após uma hora especificada.

    c.  Para definir o tamanho máximo do arquivo por arquivo de rastreamento, execute `Set @maxfilesize` . O tamanho recomendado é 200 (em MB).

    d.  Edite `@Tracefile` para definir um nome exclusivo para o arquivo de rastreamento.

    e.  Edite `@dbname` para especificar um nome de banco de dados se a carga de trabalho deve ser capturada somente em um banco de dados específico. Por padrão, a carga de trabalho em todo o servidor é capturada.

4. Para reproduzir o arquivo IRF em relação à instância de SQL Server de destino, em um prompt de comando, execute o seguinte comando:

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`

    a.  Para monitorar o status, em um prompt de comando, execute `DReplay status -f 1` .

    b.  Para interromper a reprodução, por exemplo, se você observar que a% Pass é menor do que o esperado, em um prompt de comando, execute `DReplay cancel` .

5. Interrompa a captura de rastreamento na instância de SQL Server de destino.
6. No SSMS, abra `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql` .
7. Edite `@Tracefile` para corresponder ao caminho do arquivo de rastreamento no computador de destino que executa o SQL Server.
8. Execute o script no computador de destino que executa o SQL Server.

**Usando a repetição embutida**

Se você estiver usando a reprodução incompilada, não precisará configurar Distributed Replay. A capacidade de usar a reprodução incompilada por meio da linha de comando está a caminho, mas, no ínterim, você pode usar nossa GUI para executar a reprodução usando a reprodução incompilada.

## <a name="analyze-traces-using-the-dea-command"></a>Analisar rastreamentos usando o comando DEA

Para iniciar uma nova análise de rastreamento, em um prompt de comando, execute o seguinte comando:

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -h <SQLserverInstance> -e <encryptconnection> -u <username>`

**Exemplo**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -h localhost -e`

Para exibir os relatórios de análise desses arquivos de rastreamento, você precisa usar a GUI para exibir gráficos e métricas organizadas.  No entanto, o banco de dados de análise é gravado na instância de SQL Server especificada, de modo que você também pode consultar as tabelas de análise geradas diretamente.

**Opções adicionais**

Ao analisar rastreamentos usando o comando DEA, você pode usar as seguintes opções adicionais:

| Opção| Descrição |  
| --- | --- |
| -a,--tracea | Necessária caminho do arquivo para o arquivo de evento de uma instância. Exemplo de C:\traces\Sql2008trace.trc.  Se houver um lote de arquivos, selecione o primeiro arquivo e o DEA verificará se há arquivos de substituição automaticamente. Se os arquivos estiverem em BLOB, forneça o caminho da pasta onde você deseja que os arquivos de eventos sejam armazenados localmente.  Exemplo de C:\traces\ |
| -b,--traceB | Necessária caminho do arquivo para o arquivo de evento da instância B. Exemplo de C:\traces\Sql2014trace.trc. Se houver um lote de arquivos, selecione o primeiro arquivo e o DEA verificará se há arquivos de substituição automaticamente. Se os arquivos estiverem em BLOB, forneça o caminho da pasta onde você deseja que os arquivos de eventos sejam armazenados localmente.  Exemplo de C:\traces\ |
| -r,--ReportName | Necessária nome para análise atual. O relatório de análise que é gerado será identificado por esse nome. |
| -t,--tipo | (Padrão: 0) tipo/edição do SQL Server (SqlServer = 0, AzureSQLDB = 1, Azure SQL Instância Gerenciada = 2) |
| -h,--host | Necessária SQL Server nome do host e/ou nome da instância |
| -e,--criptografar | (Padrão: true) Criptografar conexão com SQL Server instância. O padrão é verdadeiro |
| --confiar | (Padrão: false) Confiar no certificado do servidor ao conectar-se à instância do SQL Server. O padrão é falso |
| -m,--AuthMode | (Padrão: 0) modo de autenticação (Windows = 0, autenticação do SQL = 1) |
| -u,--nome de usuário | Nome de usuário para se conectar ao SQL Server |
| --p | Senha para se conectar ao SQL Server |
| --AB | (Padrão: false) O local de armazenamento do rastreamento A está em BLOB. Se usado, também deve especificar--Abu (rastrear uma URL de BLOB) |
| --BB | (Padrão: false) O local de armazenamento do rastreamento B está no BLOB. Se usado, também deve especificar--BBU (URL de blob do rastreamento B) |
| --Abu | URL de BLOB para uma instância com chave SAS |
| --BBU | URL do blob para a instância B com chave SAS |

## <a name="see-also"></a>Confira também

- Para obter mais informações sobre como usar o DEA, consulte [visão geral do assistente para experimentos de banco de dados](database-experimentation-assistant-overview.md).
