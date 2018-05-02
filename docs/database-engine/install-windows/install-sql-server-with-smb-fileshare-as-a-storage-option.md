---
title: Instalar o SQL Server com o armazenamento de compartilhamento de arquivo SMB | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8b7810b2-637e-46a3-9fe1-d055898ba639
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 72e79b62371ea42f8954c88eeecc9a779bab6487
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="install-sql-server-with-smb-fileshare-storage"></a>Instalar o SQL Server com o armazenamento de compartilhamento de arquivo SMB

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], os bancos de dados do sistema (Mestre, Modelo, MSDB e TempDB) e os bancos de dados de usuário do [!INCLUDE[ssDE](../../includes/ssde-md.md)] podem ser instalados com um servidor de arquivos SMB (protocolo SMB) como uma opção de armazenamento. Isso se aplica a instalações autônomas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a FCI (instalações de cluster de failover) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  O fluxo de arquivos não tem suporte em um compartilhamento de arquivos SMB.  
  
## <a name="installation-considerations"></a>Considerações sobre instalação  
  
### <a name="smb-fileshare-formats"></a>Formatos de compartilhamento de arquivo SMB:  
 Embora especificando o compartilhamento de arquivos SMB, os formatos de caminho a seguir têm suporte da UNC (Convenção de Nomenclatura Universal) para bancos de dados autônomos e FCI.  
  
-   \\\ServerName\ShareName\  
  
-   \\\ServerName\ShareName  
  
 Para obter mais informações sobre UNC, consulte [UNC](http://msdn.microsoft.com/library/gg465305.aspx).  
  
 O caminho UNC de loopback (um caminho UNC cujo nome de servidor é localhost, 127.0.0.1 ou o nome do computador local) não tem suporte. Como um caso especial, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o cluster de servidor de arquivos que está hospedado no mesmo nó em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executado também não tem suporte. Para impedir essa situação, é recomendável que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o cluster de servidor de arquivos seja criado em clusters do Windows separados.  
  
 Os formatos de caminho UNC abaixo não têm suporte:  
  
-   Caminho de loopback, por exemplo, \\\localhost\\..\ or \\\127.0.0.1\\...\  
  
-   Compartilhamentos administrativos, por exemplo, \\\servername\x$  
  
-   Outros formatos de caminho UNC como \\\\?\x:\  
  
-   Unidades de rede mapeadas.  
  
### <a name="supported-data-definition-language-ddl-statements"></a>Instruções DDL (linguagem de definição de dados) com suporte  
 As instruções DDL de [!INCLUDE[tsql](../../includes/tsql-md.md)] e os procedimentos armazenados de mecanismo de banco de dados a seguir dão suporte a compartilhamentos de arquivos SMB:  
  
1.  [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
2.  [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
3.  [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
4.  [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)  
  
### <a name="installation-options"></a>Opções de instalação  
  
-   Na página de interface do usuário de instalação “Configuração do Mecanismo de Banco de Dados”, guia “Diretórios de Dados”, defina o parâmetro Diretório raiz de dados como “\\\\fileserver1\share1\.”  
  
-   Na instalação do prompt de comando, especifique “/INSTALLSQLDATADIR” como “\\\fileserver1\share1\”.  
  
     Veja aqui a sintaxe de exemplo para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um servidor Autônomo usando a opção de compartilhamento de arquivos SMB:  
  
    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="<StrongPassword>" /INSTALLSQLDATADIR="\\FileServer\Share1\" /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
     Para instalar uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de nó único com o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], a instância padrão:  
  
    ```  
    setup.exe /q /ACTION=InstallFailoverCluster /InstanceName=MSSQLSERVER /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\UserName>" /ASDATADIR=<Drive>:\OLAP\Data /ASLOGDIR=<Drive>:\OLAP\Log /ASBACKUPDIR=<Drive>:\OLAP\Backup /ASCONFIGDIR=<Drive>:\OLAP\Config /ASTEMPDIR=<Drive>:\OLAP\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'" /FAILOVERCLUSTERNETWORKNAME="<Insert Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /Features=AS,SQL /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /INSTALLSQLDATADIR="\\FileServer\Share1\" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /SQLSYSADMINACCOUNTS="<DomainName\UserName> /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
     Para obter mais informações sobre o uso das várias opções de parâmetro de linha de comando no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], veja [Instalar o SQL Server 2016 por meio do Prompt de Comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
## <a name="operating-system-considerations-smb-protocol-vs-includessnoversionincludesssnoversion-mdmd"></a>Considerações sobre o sistema operacional (protocolo SMB vs. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])  
 Sistemas operacionais Windows diferentes têm versões de protocolo SMB diferentes e a versão do protocolo SMB é transparente para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode localizar os benefícios das versões diferentes do protocolo SMB com relação ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
|Sistema operacional|versão do protocolo SMB2|Benefícios do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|----------------------|---------------------------|-------------------------------------------|  
|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP 2|2.0|Desempenho aprimorado em relação a versões de SMB anteriores.<br /><br /> Durabilidade, que ajuda a recuperar de pequenos problemas de rede temporários.|  
|[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1, incluindo o Server Core|2.1|Suporte para MTU grande, que beneficia transferências de dados grandes, como backup e restauração de SQL. Este recurso deve ser habilitado pelo usuário. Para obter mais detalhes sobre como habilitar essa funcionalidade, consulte [Novidades do SMB](http://go.microsoft.com/fwlink/?LinkID=237319) (http://go.microsoft.com/fwlink/?LinkID=237319)).<br /><br /> Melhorias de desempenho significativas, especificamente para cargas de trabalho de estilo OLTP do SQL. Estas melhorias de desempenho exigem a aplicação de um hotfix. Para obter mais informações sobre o hotfix, clique [aqui](http://go.microsoft.com/fwlink/?LinkId=237320) (http://go.microsoft.com/fwlink/?LinkId=237320)).|  
|[!INCLUDE[win8srv](../../includes/win8srv-md.md)]incluindo o Server Core|3.0|O suporte para failover transparente de compartilhamentos de arquivos fornece zero tempo de inatividade sem a intervenção de administrador exigida para DBA do SQL ou administrador de servidor de arquivos em configurações do cluster de servidor de arquivos.<br /><br /> Suporte para ES usando diversas interfaces de rede simultaneamente, assim como tolerância para falhas de interface de rede.<br /><br /> Suporte para interfaces de rede com recursos de RDMA.<br /><br /> Para obter mais informações sobre esses recursos e o protocolo SMB, consulte [Visão geral do protocolo SMB](http://go.microsoft.com/fwlink/?LinkId=253174) (http://go.microsoft.com/fwlink/?LinkId=253174)).<br /><br /> Suporte SoFS (Servidor de arquivo de expansão) com disponibilidade contínua.|  
|[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2, incluindo o Server Core|3.2|O suporte para failover transparente de compartilhamentos de arquivos fornece zero tempo de inatividade sem a intervenção de administrador exigida para DBA do SQL ou administrador de servidor de arquivos em configurações do cluster de servidor de arquivos.<br /><br /> Suporte para IO usando diversas interfaces de rede simultaneamente, assim como tolerância para falhas de interface de rede, usando SMB Multichannel.<br /><br /> Suporte para interfaces de rede com recursos de RDMA usando SMB Direct.<br /><br /> Para obter mais informações sobre esses recursos e o protocolo SMB, consulte [Visão geral do protocolo SMB](http://go.microsoft.com/fwlink/?LinkId=253174) (http://go.microsoft.com/fwlink/?LinkId=253174)).<br /><br /> Suporte SoFS (Servidor de arquivo de expansão) com disponibilidade contínua.<br /><br /> Otimizado para leitura/gravação aleatória pequena de E/S comum para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLTP.<br /><br /> O MTU (Unidade de transmissão máxima) é ativado por padrão, o que melhora significativamente o desempenho em grandes transferências sequenciais como data warehouse do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o backup de banco de dados ou restauração.|  
  
## <a name="security-considerations"></a>Considerações sobre segurança  
  
-   A conta de serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a conta de serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent devem ter as permissões de compartilhamento FULL CONTROL e permissões NTFS nas pastas de compartilhamento SMB. A conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser uma conta de domínio ou uma conta de sistema se for usado um servidor de arquivos SMB. Para obter mais informações sobre permissões de compartilhamento e NTFS, consulte [Permissões de compartilhamento e NTFS em um servidor de arquivos](http://go.microsoft.com/fwlink/?LinkId=245535) (http://go.microsoft.com/fwlink/?LinkId=245535)).  
  
    > [!NOTE]  
    >  As permissões de compartilhamento FULL CONTROL e as permissões NTFS nas pastas de compartilhamento SMB devem ser restritas a: conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e usuários do Windows com funções de servidor admin.  
  
     Era recomendado usar a conta de domínio como uma conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se a conta do sistema for usada como uma conta de serviço, conceda as permissões para a conta do computador no formato: \<*domain_name*>\\<*computer_name*>\*$*.  
  
    > [!NOTE]  
    >  Durante instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], será necessário especificar a conta de domínio como uma conta de serviço se o compartilhamento de arquivos SMB for especificado como uma opção de armazenamento. Com o compartilhamento de arquivos SMB, a conta de Sistema somente poderá ser especificada como uma conta de serviço após a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
    >   
    >  Contas virtuais não podem ser autenticadas em um local remoto. Todas as contas virtuais usam a permissão da conta de máquina. Provisione a conta do computador no formato \<*domain_name*>\\<*computer_name*>\*$*.  
  
-   A conta usada para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter permissões FULL CONTROL na pasta de compartilhamento de arquivos SMB usada como o diretório de dados ou qualquer outra pasta de dados (diretório de banco de dados de usuário, diretório de log de banco de dados de usuário, diretório de TempDB, diretório de log TempDB, diretório de backup) durante a instalação de cluster.  
  
-   A conta usada para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter privilégios SeSecurityPrivilege no servidor de arquivos SMB. Para conceder esse privilégio, use o console Política de Segurança Local no servidor de arquivos para adicionar a conta de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à política Gerenciar a auditoria e o log de segurança. Essa configuração está disponível na seção Atribuições de Direitos do Usuário, em Políticas Locais, no console Política de Segurança Local.  
  
## <a name="known-issues"></a>Problemas conhecidos  
  
-   Ao desanexar um banco de dados do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que reside no armazenamento anexado por rede, você poderá ter um problema de permissão de banco de dados ao tentar reanexar o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O problema é definido [neste artigo da base de dados](http://go.microsoft.com/fwlink/?LinkId=237321) (http://go.microsoft.com/fwlink/?LinkId=237321)). Para resolver este problema, consulte a seção **Mais Informações** no artigo da Base de Dados de Conhecimento.  
  
-   Se o compartilhamento de arquivos SMB é usado como uma opção de armazenamento para uma instância clusterizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por padrão o log de diagnóstico do cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode ser gravado no compartilhamento de arquivos porque a DLL de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tem a permissão de leitura/gravação no compartilhamento de arquivos. Para resolver esse problema, tente um dos seguintes métodos:  
  
    1.  Conceda permissões de leitura/gravação no compartilhamento de arquivos a todos os objetos de computador no cluster.  
  
    2.  Defina o local dos logs de diagnóstico como um caminho de arquivo local. Consulte o seguinte exemplo:  
  
        ```sql  
        ALTER SERVER CONFIGURATION  
        SET DIAGNOSTICS LOG PATH = 'C:\logs';  
        ```  
  
## <a name="see-also"></a>Confira também  
 [Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
