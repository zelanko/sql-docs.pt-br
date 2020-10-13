---
description: MSSQLSERVER_17207
title: MSSQLSERVER_17207
ms.custom: ''
ms.date: 07/25/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: ''
author: PijoCoder
ms.author: mathoma
ms.openlocfilehash: d1c0face9315a38d4748cffef71e135401102dd0
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869462"
---
# <a name="mssqlserver_17207"></a>MSSQLSERVER_17207
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |
| :-------- | :---- |
|Nome do Produto|SQL Server|  
|ID do evento|17207|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBLKIO_OS2DISKERROR|  
|Texto da mensagem|%ls: erro de sistema operacional %ls durante criação ou abertura do arquivo '%ls'. Faça o diagnóstico, corrija o erro e tente novamente a operação.|  


## <a name="explanation"></a>Explicação  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pôde abrir o arquivo indicado devido ao erro de sistema operacional especificado.  

Você pode ver o erro 17207 no Evento de aplicativos do Windows ou no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode abrir arquivos de log de transações e/ou de banco de dados. Este é um exemplo da aparência do erro.

``` 
Error: 17207, Severity: 16, State: 1.
FileMgr::StartSecondaryDataFiles: Operating system error 2(The system cannot find the file specified.) occurred while creating or opening file 'F:\MSSQL\DATA\MyDB_FG1_1.ndf'. Diagnose and correct the operating system error, and retry the operation.
```

Você pode ver esses erros durante o processo de inicialização da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou qualquer operação de banco de dados que tente iniciar o banco de dados (por exemplo, ALTER DATABASE). Em alguns cenários, você poderá ver os erros 17207 e 17204 e, em outras ocasiões, verá apenas um deles.

Se um banco de dados de usuário em execução encontrar esses erros, o banco de dados será deixado no estado de RECOVERY_PENDING e os aplicativos não poderão acessar o banco de dados. Se um banco de dados do sistema encontrar esses erros, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não será iniciada, e você não poderá se conectar a essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso também pode fazer com que um recurso de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fique offline.

Se o problema estiver relacionado ao grupo de arquivos FileStream do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você observará que apenas o caminho completo do diretório está listado, em vez de um nome de arquivo. Veja um exemplo. 
```
Error: 17207, Severity: 16, State: 1.
STREAMFCB::Startup: Operating system error 2(The system cannot find the file specified.) occurred while creating or opening file 'C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\DATA\bpa_files_test_fs_1\bpa_files_test_fs_1'. Diagnose and correct the operating system error, and retry the operation.
```

## <a name="cause"></a>Causa
Antes que qualquer banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possa ser usado, o banco de dados precisa ser iniciado. O processo de inicialização do banco de dados envolve iniciar várias estruturas de dados que representam o banco de dados e os arquivos dele, abrir todos os arquivos que pertencem ao banco de dados e, por fim, executar a recuperação no banco de dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa a função da API do Windows [CreateFile](/windows/win32/api/fileapi/nf-fileapi-createfilea) para abrir os arquivos que pertencem a um banco de dados.
 
As mensagens 17207 (e 17204) indicam que um erro foi encontrado quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tentou abrir os arquivos de banco de dados durante o processo de inicialização.
 
Essas mensagens de erro contêm as seguintes informações:
1. Nome da função do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está tentando abrir o arquivo. O nome da função que você normalmente observa nas mensagens de erro é um dos seguintes:
   - FCB::Open                               – o arquivo encontrou um erro quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tentou abri-lo
   - FileMgr::StartPrimaryDataFiles         – um arquivo de dados primário ou um arquivo pertencente ao grupo de arquivo primário
   - FileMgr::StartSecondaryDataFiles         – um arquivo pertencente a um grupo de arquivo secundário
   - FileMgr::StartLogFiles         – um arquivo de log de transações
   - STREAMFCB::Startup              – um contêiner de FileStream do SQL
   - FCB::RemoveAlternateStreams
  
      
1. As informações de estado distinguem vários locais dentro de uma função que pode gerar essa mensagem de erro.
1. O caminho físico completo para o arquivo.
1. A ID do arquivo correspondente ao arquivo.
1. O código de erro do sistema operacional e a descrição do erro. Em alguns casos, você verá apenas o código de erro.
 
As informações de erro do sistema operacional impressas nessas mensagens de erro são a causa raiz que leva ao erro 17204. As causas comuns para essas mensagens de erro são um problema de permissão ou um caminho incorreto para o arquivo.


## <a name="user-action"></a>Ação do usuário  
1. A resolução do erro 17207 envolve a compreensão do código de erro do sistema operacional associado e o diagnóstico desse erro. Depois que a condição de erro do sistema operacional for resolvida, você poderá tentar reiniciar o banco de dados (por exemplo, usando ALTER DATABASE SET ONLINE) ou a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para colocar o banco de dados afetado online. Em alguns casos, talvez você não consiga resolver o erro do sistema operacional. Portanto, precisará executar ações corretivas específicas. Discutiremos tais ações nesta seção.
1. Se a mensagem de erro 17207 contiver apenas um código de erro e não uma descrição de erro, você poderá tentar resolver esse código usando o comando de shell do sistema operacional: net helpmsg <error code>. Se você receber um código de status de 8 dígitos como o código de erro, poderá consultar as fontes de informações em [Como converter um HRESULT em um código de erro Win32?](https://devblogs.microsoft.com/oldnewthing/20061103-07/?p=29133) para decodificar quais são esses códigos de status em erros de sistema operacional.
1. Se você receber o erro do sistema operacional ```Access is Denied``` = 5, considere estes métodos:
   -  Verifique se as permissões estão definidas no arquivo examinando as propriedades dele no Windows Explorer. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa grupos do Windows para provisionar o controle de acesso em vários recursos do arquivo. Verifique se o grupo apropriado (com nomes como SQLServerMSSQLUser$ComputerName$MSSQLSERVER ou SQLServerMSSQLUser$ComputerName$InstanceName) tem as permissões necessárias no arquivo de banco de dados mencionado na mensagem de erro. Para obter mais informações, confira [Configurar permissões do sistema de arquivos para acesso ao Mecanismo de Banco de Dados](/previous-versions/sql/2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access?view=sql-server-2014). Verifique se o grupo do Windows realmente inclui a conta de inicialização do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o SID do serviço.
   -  Examine a conta de usuário na qual o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está atualmente em execução. Você pode usar o Gerenciador de Tarefas do Windows para obter essas informações. Procure o valor de "Nome de Usuário" para o executável "sqlservr.exe". Além disso, se você alterou recentemente a conta de serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], saiba que a maneira com suporte para realizar essa operação é usar o utilitário SQL Server Configuration Manager. Mais informações sobre isso estão disponíveis em [SQL Server Configuration Manager](../sql-server-configuration-manager.md). 
   -  Dependendo do tipo de operação, abrir bancos de dados durante a inicialização do servidor, anexar um banco de dados, restaurar o banco de dados etc., a conta usada para representação e acesso ao arquivo de banco de dados pode variar. Examine o tópico [Proteger arquivos de log e dados](/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105)) para entender qual operação define qual permissão e de quais contas. Use uma ferramenta como [Monitor do Processo](/sysinternals/downloads/procmon) do SysInternals do Windows para entender se o acesso ao arquivo está acontecendo no contexto de segurança da conta de inicialização do serviço (ou SID do serviço) da instância do SQL Server ou de uma conta representada.

      Se o SQL Server estiver representando as credenciais de usuário do logon que executa a operação ALTER DATABASE ou CREATE DATABASE, você observará as informações a seguir na ferramenta Monitor do Processo (um exemplo).

        ```
        Date & Time:      3/27/2010 8:26:08 PM
        Event Class:        File System
        Operation:          CreateFile
        Result:                ACCESS DENIED
        Path:                  C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\DATA\attach_test.mdf
        TID:                   4288
        Duration:             0.0000366
        Desired Access:Generic Read/Write
        Disposition:        Open
        Options:            Synchronous IO Non-Alert, Non-Directory File, Open No Recall
        Attributes:          N
        ShareMode:       Read
        AllocationSize:   n/a
        Impersonating: DomainName\UserName
        ```
  
1. Se você estiver obtendo o erro de SO `The system cannot find the file specified` = 3:
   - Examine o caminho completo da mensagem de erro.
   - Verifique se a unidade de disco e o caminho da pasta estão visíveis e acessíveis no Windows Explorer.
   - Examine o log de eventos do Windows para descobrir se existem problemas com essa unidade de disco.
   - Se o caminho estiver incorreto e se esse banco de dados já existir no sistema, você poderá alterar os caminhos do arquivo de banco de dados usando os métodos explicados no artigo [Mover arquivos de banco de dados](../databases/move-database-files.md). Talvez você precise usar este procedimento, especialmente para arquivos de banco de dados do sistema que encontrem 17204 ou 17207 e se você estiver trabalhando em um cenário de recuperação de desastre em que as unidades de disco especificadas não estão disponíveis. Este tópico também explica como você pode identificar a localização atual dos vários bancos de dados do sistema [mestre, modelo, tempdb, msdb e mssqlsystemresource].
   - Se você vir esse erro porque os arquivos de banco de dados estão ausentes, será necessário restaurar o banco de dados de um backup válido:
     - Se o arquivo de banco de dados associado ao erro pertencer a um grupo de arquivos secundário, você poderá, opcionalmente, marcar esse grupo de arquivos offline, colocar o banco de dados online e executar uma restauração somente desse grupo de arquivos. Para obter mais informações, confira a seção OFFLINE do tópico [Opções de arquivo e grupo de arquivos ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).
     - Se o arquivo que produziu o erro for um arquivo de log de transações, examine as informações nas seções "FOR ATTACH" e "FOR ATTACH_REBUILD_LOG" do tópico [CRIAR BANCO DE DADOS (Transact-SQL)](../../t-sql/statements/create-database-transact-sql.md) para entender como você pode recriar os arquivos de log de transações ausentes.
   - Verifique se alguma localização de rede ou disco [como unidade iSCSI] está disponível antes que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tente acessar os arquivos de banco de dados nesses locais. Se necessário, crie as dependências exigidas no Administrador de Cluster ou no Gerenciador de Controle de Serviço.

1. Se você estiver recebendo o erro de sistema operacional `The process cannot access the file because it is being used by another process` = 32:
   - Use uma ferramenta como o [Explorador de Processos](/sysinternals/downloads/process-explorer) ou o [Identificador](/sysinternals/downloads/handle) do Windows Sysinternals para descobrir se outro processo ou serviço adquiriu bloqueio exclusivo nesse arquivo de banco de dados.
   - Interrompa o acesso desse processo aos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Arquivos de banco de dados. Exemplos comuns incluem programas antivírus (confira as diretrizes para exclusões de arquivo no [artigo da base de dados](https://support.microsoft.com/help/309422/choosing-antivirus-software-for-computers-that-run-sql-server) a seguir).
   - Em um ambiente de cluster, verifique se o processo sqlservr.exe do nó proprietário anterior realmente liberou os identificadores para os arquivos de banco de dados. Normalmente, isso não ocorre, mas as configurações incorretas do cluster ou dos caminhos de E/S podem levar a esses problemas.
