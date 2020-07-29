---
title: MSSQLSERVER_17204 | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: 40db66f9-dd5e-478c-891e-a06d363a2552
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a094a2baf20ccdf29514a82f4ff749c6d9e18be3
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87235985"
---
# <a name="mssqlserver_17204"></a>MSSQLSERVER_17204
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |
| :-------- | :---- |
|Nome do Produto|SQL Server|  
|ID do evento|17204|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBLKIO_DEVOPENFAILED|  
|Texto da mensagem|%ls: não foi possível abrir arquivo %ls para o número de arquivo %d.  Erro de SO: %ls.|  
  
## <a name="explanation"></a>Explicação  
O SQL Server não pôde abrir o arquivo indicado devido ao erro de sistema operacional especificado.  

Você pode ver o erro 17204 no evento de aplicativo do Windows ou o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando o SQL Server não pode abrir arquivos de log de transações e/ou de banco de dados. Este é um exemplo da aparência do erro:

``` 
Error: 17204, Severity: 16, State: 1.
FCB::Open failed: Could not open file c:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\data\MyDB_Prm.mdf for file number 1.  OS error: 5(Access is denied.).
```

Você pode ver esses erros durante o processo de inicialização da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou qualquer operação de banco de dados que tente iniciar o banco de dados (por exemplo, ALTER DATABASE). Em alguns cenários, você poderá ver os erros 17204 e 17207 e, em outras ocasiões, poderá ver apenas um deles.

Se um banco de dados de usuário em execução encontrar esses erros, o banco de dados será deixado no estado de RECOVERY_PENDING, e os aplicativos não poderão acessar o banco de dados. Se um banco de dados do sistema encontrar esses erros, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não será iniciada, e você não poderá se conectar a essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Uma falha em um banco de dados do sistema também pode fazer com que um recurso do cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fique offline.

## <a name="cause"></a>Causa
Antes que qualquer banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possa ser usado, o banco de dados precisa ser iniciado. O processo de inicialização do banco de dados envolve: 
1. Inicializar várias estruturas de dados que representam o banco de dados e os arquivos do banco de dados
1. Abrir todos os arquivos que pertencem ao banco de dados
1. Executar a recuperação no banco de dados 

O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa a função da API do Windows [CreateFile](https://docs.microsoft.com/windows/win32/api/fileapi/nf-fileapi-createfilea) para abrir os arquivos que pertencem a um banco de dados.
 
As mensagens 17204 (e 17207) indicam que um erro foi encontrado quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tentou abrir os arquivos de banco de dados durante o processo de inicialização.
 
Essas mensagens de erro contêm as seguintes informações:
1. Nome da função do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está tentando abrir o arquivo. O nome da função que você normalmente observa nas mensagens de erro é um dos seguintes:
   - FCB::Open – ocorreu um erro com o arquivo quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tentou abri-lo
   - FileMgr::StartPrimaryDataFiles – um arquivo de dados primário ou um arquivo pertencente ao grupo de arquivo primário
   - FileMgr::StartSecondaryDataFiles – um arquivo que pertence a um grupo de arquivo secundário
   - FileMgr::StartLogFiles – um arquivo de log de transações
   - STREAMFCB::Startup – um contêiner de FileStream do SQL
   - FCB::RemoveAlternateStreams
  
      
1. As informações de estado distinguem vários locais dentro de uma função que pode gerar essa mensagem de erro
1. O caminho físico completo para o arquivo
1. A ID do arquivo correspondente ao arquivo
1. O código de erro do sistema operacional e a descrição do erro. Em alguns casos, você verá apenas o código de erro.
 
As informações de erro do sistema operacional impressas nessas mensagens de erro são a causa raiz que leva ao erro 17204. As causas comuns para essas mensagens de erro são um problema de permissão ou um caminho incorreto para o arquivo.


## <a name="user-action"></a>Ação do usuário  
1. A resolução do erro 17204 envolve a compreensão do código de erro do sistema operacional associado e o diagnóstico desse erro. Depois que a condição de erro do sistema operacional for resolvida, você poderá tentar reiniciar o banco de dados (por exemplo, usando ALTER DATABASE SET ONLINE) ou a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para colocar o banco de dados afetado online. Em alguns casos, talvez você não consiga resolver o erro do sistema operacional. Portanto, precisará realizar ações corretivas específicas. Discutiremos tais ações nesta seção.
1. Se a mensagem de erro 17204 contiver apenas um código de erro e não uma descrição de erro, você poderá tentar resolver o código de erro usando o comando de shell do sistema operacional: net helpmsg <error code>. Se você receber um código de status de 8 dígitos como o código de erro, poderá consultar as fontes de informações em [Como converter um HRESULT em um código de erro Win32?](https://devblogs.microsoft.com/oldnewthing/20061103-07/?p=29133) para decodificar quais são esses códigos de status em erros de sistema operacional.
1. Se você receber o erro do sistema operacional `Access is Denied` = 5, considere estes métodos:
   -  Verifique se as permissões estão definidas no arquivo examinando as propriedades dele no Windows Explorer. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa grupos do Windows para provisionar o Controle de Acesso em vários recursos do arquivo. Verifique se o grupo apropriado [com nomes como SQLServerMSSQLUser$ComputerName$MSSQLSERVER ou SQLServerMSSQLUser$ComputerName$InstanceName] tem as permissões necessárias no arquivo de banco de dados mencionado na mensagem de erro. Para obter mais informações, confira [Configurar permissões do sistema de arquivos para acesso ao Mecanismo de Banco de Dados](/previous-versions/sql/2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access?view=sql-server-2014). Verifique se o grupo do Windows realmente inclui a conta de inicialização do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o SID do serviço.
   -  Examine a conta de usuário na qual o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está atualmente em execução. Você pode usar o Gerenciador de Tarefas do Windows para obter essas informações. Procure o valor de "Nome de Usuário" para o executável "sqlservr.exe". Além disso, se você alterou recentemente a conta de serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], saiba que a maneira com suporte para realizar essa operação é por meio do utilitário SQL Server Configuration Manager. Mais informações sobre isso estão disponíveis em [SQL Server Configuration Manager](../sql-server-configuration-manager.md). 
   -  Dependendo do tipo de operação – abrir bancos de dados durante a inicialização do servidor, anexar um banco de dados, restaurar o banco de dados etc. – a conta usada para representação e acesso ao arquivo de banco de dados pode variar. Examine o tópico [Proteger arquivos de log e dados](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105)?redirectedfrom=MSDN) para entender qual operação define qual permissão e de quais contas. Use uma ferramenta como [Monitor do Processo](https://docs.microsoft.com/sysinternals/downloads/procmon) do SysInternals do Windows para entender se o acesso ao arquivo está acontecendo no contexto de segurança da conta de inicialização do serviço (ou SID do serviço) da instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou de uma conta representada.

      Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver representando as credenciais do usuário que executa a operação ALTER DATABASE ou CREATE DATABASE, você observará as seguintes informações na ferramenta Monitor do Processo (um exemplo):
        ```Date & Time:      3/27/2010 8:26:08 PM
        Event Class:        File System
        Operation:          CreateFile
        Result:                ACCESS DENIED
        Path:                  C:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\DATA\attach_test.mdf
        TID:                   4288
        Duration:             0.0000366
        Desired Access:Generic Read/Write
        Disposition:        Open
        Options:            Synchronous IO Non-Alert, Non-Directory File, Open No Recall
        Attributes:          N
        ShareMode:       Read
        AllocationSize:   n/a
        Impersonating: DomainName\UserName```
  
1. If you are getting `The system cannot find the file specified` OS error = 3:
   - Review the complete path from the error message
   - Ensure the disk drive and the folder path is visible and accessible from Windows Explorer
   - Review the Windows Event log to find out if any problems exist with this disk drive
   - If the path is incorrect and if this database already exists in the system, you can change the database file paths using the methods explained in the topic [Move Database Files](../databases/move-database-files.md). You may have to use this procedure, especially for system database files that encounter 17204 or 17207 and you are working through a disaster recovery scenario where the specified disk drives are unavailable. This topic also explains how you can identify the current location of the various system databases [master, model, tempdb, msdb and mssqlsystemresource].
   - If you see this error because the database files are missing, you have to restore the database from a valid backup.
     - If the database file associated with the error belongs to a secondary filegroup, then you can optionally mark that filegroup offline, bring the database online and then perform a restore of that filegroup alone. For more information, refer to the OFFLINE section of the topic [ALTER DATABASE File and Filegroup Options (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).
     - If the file that produced the error is a transaction log file, review the information under the sections "FOR ATTACH" and "FOR ATTACH_REBUILD_LOG" of the topic [CREATE DATABASE (Transact-SQL)](../../t-sql/statements/create-database-transact-sql.md) to understand how you can recreate the missing transaction log files.
   - Ensure that any disk or network location [like iSCSI drive] is available before [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attempts to access the database files on these locations. If needed create the required dependencies in Cluster Administrator or Service Control Manager.
1. If you're getting the `The process cannot access the file because it is being used by another process` operating system error = 32:
   - Use a tool like [Process Explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer) or [Handle](https://docs.microsoft.com/sysinternals/downloads/handle) from Windows Sysinternals to find out if another process or service has acquired exclusive lock on this database file
   - Stop that process from accessing [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database files. Common examples include anti-virus programs (see guidance for file exclusions in the following [KB article](https://support.microsoft.com/help/309422/choosing-antivirus-software-for-computers-that-run-sql-server) )
   - In a cluster environment, make sure that the sqlservr.exe process from the previous owning node has actually released the handles to the database files. Normally, this doesn't occur, but misconfigurations of the cluster or I/O paths can lead to such issues.
  
