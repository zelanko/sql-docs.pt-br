---
title: MSSQLSERVER_5120
ms.custom: ''
ms.date: 07/25/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5120 (Database Engine error)
ms.assetid: ''
author: PijoCoder
ms.author: mathoma
ms.openlocfilehash: eab5970a6dd7e8fa136621a28d1f697461b33712
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246565"
---
# <a name="mssqlserver_5120"></a>MSSQLSERVER_5120
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|5120|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DSK_FCB_FAILURE|  
|Texto da mensagem|Erro de tabela: Não é possível abrir o arquivo físico "%.*ls". Erro no sistema operacional %d: “%ls”.|  
  
## <a name="explanation"></a>Explicação  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não conseguiu abrir um arquivo de banco de dados.  O erro do sistema operacional fornecido na mensagem aponta para os motivos subjacentes mais específicos da falha. Normalmente, você pode ver esse erro junto com outros, como [17204](mssqlserver-17204-database-engine-error.md) ou [17207](mssqlserver-17207-database-engine-error.md).
  
## <a name="user-action"></a>Ação do usuário  
  
  Faça o diagnóstico, corrija o erro e, em seguida, tente novamente a operação. Existem vários estados que podem ajudar a Microsoft a restringir a área de ocorrência no produto. 
  
### <a name="access-is-denied"></a>Acesso negado 
Se você receber o erro do sistema operacional `Access is Denied` = 5, considere estes métodos:
   -  Verifique se as permissões estão definidas no arquivo examinando as propriedades dele no Windows Explorer. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa grupos do Windows para provisionar o Controle de Acesso em vários recursos do arquivo. Verifique se o grupo apropriado [com nomes como SQLServerMSSQLUser$ComputerName$MSSQLSERVER ou SQLServerMSSQLUser$ComputerName$InstanceName] tem as permissões necessárias no arquivo de banco de dados mencionado na mensagem de erro. Para obter mais informações, confira [Configurar permissões do sistema de arquivos para acesso ao Mecanismo de Banco de Dados](/previous-versions/sql/2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access?view=sql-server-2014). Verifique se o grupo do Windows realmente inclui a conta de inicialização do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o SID do serviço.
   -  Examine a conta de usuário na qual o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está atualmente em execução. Você pode usar o Gerenciador de Tarefas do Windows para obter essas informações. Procure o valor de "Nome de Usuário" para o executável "sqlservr.exe". Além disso, se você alterou recentemente a conta de serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], saiba que a maneira com suporte para realizar essa operação é usar o utilitário [SQL Server Configuration Manager](../sql-server-configuration-manager.md). 
   -  Dependendo do tipo de operação, abrir bancos de dados durante a inicialização do servidor, anexar um banco de dados, restaurar o banco de dados etc., a conta usada para representação e acesso ao arquivo de banco de dados pode variar. Examine o tópico [Proteger arquivos de log e dados](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105)?redirectedfrom=MSDN) para entender qual operação define qual permissão e de quais contas. Use uma ferramenta como [Monitor do Processo](https://docs.microsoft.com/sysinternals/downloads/procmon) do SysInternals do Windows para entender se o acesso ao arquivo está acontecendo no contexto de segurança da conta de inicialização do serviço (ou SID do serviço) da instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou de uma conta representada.

      Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver representando as credenciais de usuário do logon que executa a operação ALTER DATABASE ou CREATE DATABASE, você observará as informações a seguir na ferramenta Monitor do Processo (um exemplo).
      
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
  
  
### <a name="attaching-files-that-reside-on-a-network-attached-storage"></a>Como anexar arquivos que residem em um NAS  
Se você não puder anexar novamente um banco de dados que resida no NAS, uma mensagem como esta poderá ser registrada no log do aplicativo.

`Msg 5120, Level 16, State 101, Line 1 Unable to open the physical file "\\servername\sharename\filename.mdf". Operating system error 5: (Access is denied.).`

Esse problema ocorre porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] redefine as permissões de arquivo quando o banco de dados é desanexado. Quando você tenta anexar novamente o banco de dados, ocorre uma falha devido a permissões de compartilhamento limitadas.

Para resolver o problema, siga estas etapas:
1. Use a opção de inicialização -T para iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use essa opção de inicialização para ativar o sinalizador de rastreamento 1802 no [SQL Server Configuration Manager](../sql-server-configuration-manager.md) (confira [Sinalizadores de Rastreamento](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md) para obter informações sobre o 1802). Para obter mais informações sobre como alterar os parâmetros de inicialização, confira [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md).

2. Use o comando a seguir para desanexar o banco de dados.
   ```sql
    exec sp_detach_db DatabaseName
    go 
   ```

3. Use o comando a seguir para reconectar o banco de dados.
   ```sql
   exec sp_attach_db DatabaseName, '\\Network-attached storage_Path\DatabaseMDFFile.mdf', '\\Network-attached storage_Path\DatabaseLDFFile.ldf'
   go
   ```
 
