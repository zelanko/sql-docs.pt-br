---
title: Recompilar bancos de dados do sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- master database [SQL Server], rebuilding
- REBUILDDATABASE parameter
- rebuilding databases, master
- system databases [SQL Server], rebuilding
ms.assetid: af457ecd-523e-4809-9652-bdf2e81bd876
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9cca83a20c7559a8b7192fd345b559226c9c7d57
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135496"
---
# <a name="rebuild-system-databases"></a>Recriar bancos de dados do sistema
  Os bancos de dados do sistema devem ser recriados para corrigir problemas de corrupção nos bancos de dados do sistema [master](master-database.md), [model](model-database.md), [msdb](msdb-database.md)ou [resource](resource-database.md) , ou para modificar o agrupamento em nível de servidor padrão. Este tópico fornece instruções passo a passo para recriar bancos de dados do sistema no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Pré-requisitos](#Prerequisites)  
  
-   **Procedimentos:**  
  
     [Recriar bancos de dados do sistema](#RebuildProcedure)  
  
     [Recriar o banco de dados de recursos](#Resource)  
  
     [Criar um novo banco de dados msdb](#CreateMSDB)  
  
-   **Acompanhamento:**  
  
     [Solução de problemas de erros de recriação](#Troubleshoot)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 Quando os bancos de dados do sistema mestre, modelo, msdb e tempdb são recriados, os bancos de dados são descartados e recriados em seu local original. Se um agrupamento novo for especificado na instrução REBUILD, os bancos de dados do sistema serão criados usando essa configuração de agrupamento. Todas as modificações do usuário nesses bancos de dados são perdidas. Por exemplo, você pode ter objetos definidos pelo usuário no banco de dados mestre, trabalhos agendados no msdb ou alterações nas configurações padrão do banco de dados modelo.  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Execute as tarefas a seguir antes de recriar os bancos de dados do sistema para garantir que os bancos de dados possam ser restaurados para suas configurações atuais.  
  
1.  Registre todos os valores de configuração em todo o servidor.  
  
    ```  
    SELECT * FROM sys.configurations;  
    ```  
  
2.  Registre todos os pacotes de serviço e os hotfixes aplicados à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao agrupamento atual. Você deve reaplicar essas atualizações depois de recriar os bancos de dados do sistema.  
  
    ```  
    SELECT  
    SERVERPROPERTY('ProductVersion ') AS ProductVersion,  
    SERVERPROPERTY('ProductLevel') AS ProductLevel,  
    SERVERPROPERTY('ResourceVersion') AS ResourceVersion,  
    SERVERPROPERTY('ResourceLastUpdateDateTime') AS ResourceLastUpdateDateTime,  
    SERVERPROPERTY('Collation') AS Collation;  
    ```  
  
3.  Registre o local atual de todos os arquivos de log e de dados nos bancos de dados do sistema. A recriação do bancos de dados do sistema instala todos os bancos de dados do sistema em seu local original. Se você tiver movido os arquivos de log ou de dados do banco de dados do sistema para um local diferente, mova os arquivos novamente.  
  
    ```  
    SELECT name, physical_name AS current_file_location  
    FROM sys.master_files  
    WHERE database_id IN (DB_ID('master'), DB_ID('model'), DB_ID('msdb'), DB_ID('tempdb'));  
    ```  
  
4.  Localize o backup atual dos bancos de dados mestre, modelo e msdb.  
  
5.  Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver configurada como um Distribuidor de replicação, localize o backup atual do banco de dados de distribuição.  
  
6.  Verifique se você possui as permissões adequadas para recriar os bancos de dados do sistema. Para executar essa operação, você deve ser membro da função de servidor fixa `sysadmin`. Para obter mais informações, veja [Funções de nível de servidor](../security/authentication-access/server-level-roles.md).  
  
7.  Verifique se as cópias dos arquivos de log modelo do mestre, do modelo e do msdb existem no servidor local. O local padrão dos arquivos de modelo é C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn\Templates. Esses arquivos são usados durante o processo de recriação e devem estar presentes para que a Instalação tenha êxito. Se eles estiverem ausentes, execute o recurso de Instalação Reparar ou copie os arquivos manualmente da mídia de instalação. Para localizar os arquivos na mídia de instalação, navegue até o diretório da plataforma adequada (x86 ou x64) e, em seguida, navegue até setup\sql_engine_core_inst_msi\Pfiles\SqlServr\MSSQL.X\MSSQL\Binn\Templates.  
  
##  <a name="RebuildProcedure"></a> Recriar bancos de dados do sistema  
 O procedimento a seguir recria os bancos de dados do sistema mestre, modelo, msdb e tempdb. Você não pode especificar os bancos de dados do sistema que devem ser recriados. Para instâncias clusterizadas, esse procedimento deve ser executado no nó ativo, e o recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no grupo de aplicativos de cluster correspondente deve estar offline antes da execução do procedimento.  
  
 Esse procedimento não recria o banco de dados de recursos. Consulte a seção, "Procedimento de recriação do banco de dados de recursos" mais adiante neste tópico.  
  
#### <a name="to-rebuild-system-databases-for-an-instance-of-sql-server"></a>Para recriar os bancos de dados do sistema para uma instância do SQL Server:  
  
1.  Insira a mídia de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] na unidade de disco ou, em um prompt de comando, altere o diretório para o local do arquivo setup.exe no servidor local. O local padrão no servidor é C:\Arquivos de Programas\Microsoft SQL Server\120\Setup Bootstrap\Release.  
  
2.  Em uma janela de prompt de comando, digite o comando a seguir. São usados colchetes para indicar parâmetros opcionais. Não digite os colchetes. Ao usar um sistema operacional Windows com UAC (Controle de Conta de Usuário) habilitado, a execução da Instalação exige privilégios elevados. O prompt de comando deve ser executado como Administrador.  
  
     `Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName /SQLSYSADMINACCOUNTS=accounts [ /SAPWD= StrongPassword ] [ /SQLCOLLATION=CollationName]`  
  
    |Nome do parâmetro|Description|  
    |--------------------|-----------------|  
    |/QUIET ou /Q|Especifica que a Instalação é executada sem nenhuma interface do usuário.|  
    |/ACTION=REBUILDDATABASE|Especifica que Instalação recria os bancos de dados do sistema.|  
    |/INSTANCENAME=*InstanceName*|É o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para a instância padrão, digite MSSQLSERVER.|  
    |/SQLSYSADMINACCOUNTS =*contas*|Especifica os grupos do Windows ou contas individuais para adicionar ao `sysadmin` função de servidor fixa. Ao especificar mais de uma conta, separe as contas com um espaço em branco. Por exemplo, digite **BUILTIN\Administrators MyDomain\MyUser**. Quando você estiver especificando uma conta que contém um espaço em branco dentro do nome de conta, coloque a conta entre aspas duplas. Por exemplo, digite `NT AUTHORITY\SYSTEM`.|  
    |[ /SAPWD=*StrongPassword* ]|Especifica a senha da conta `sa` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse parâmetro será exigido se a instância usar o modo de Autenticação Mista (Autenticação do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows).<br /><br /> **\*\* Observação de segurança \* \***  o `sa` conta é um conhecido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta e geralmente é visada por usuários mal-intencionados. É muito importante que você use uma senha forte para o `sa` logon.<br /><br /> Não especifique esse parâmetro para o modo de Autenticação do Windows.|  
    |[ /SQLCOLLATION=*CollationName* ]|Especifica um novo agrupamento no nível do servidor. Esse parâmetro é opcional. Quando não está especificado, o agrupamento atual do servidor é usado.<br /><br /> **\*\* Importante \* \***  alterando o agrupamento de nível de servidor não altera o agrupamento de bancos de dados de usuário existentes. Por padrão, todos os bancos de dados do usuário criados recentemente usarão o novo agrupamento.<br /><br /> Para obter mais informações, veja [Definir ou alterar o agrupamento do servidor](../collations/set-or-change-the-server-collation.md).|  
  
3.  Quando a Instalação tiver concluído a recriação dos bancos de dados do sistema, ela retornará ao prompt de comando sem mensagens. Examine o arquivo de log Summary.txt para verificar se o processo foi concluído com êxito. Esse arquivo está localizado em C:\Arquivos de Programas\Microsoft SQL Server\120\Setup Bootstrap\Logs.  
  
## <a name="post-rebuild-tasks"></a>Tarefas pós-recriação  
 Depois de recriar o banco de dados, talvez seja necessário executar as tarefas adicionais a seguir:  
  
-   Restaure os backups completos mais recentes dos bancos de dados mestre, modelo e msdb. Para obter mais informações, consulte [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
    > [!IMPORTANT]  
    >  Se você alterou o agrupamento do servidor, não restaure os bancos de dados do sistema. Fazer isso substituirá o novo agrupamento pela configuração do agrupamento anterior.  
  
     Se um backup não estiver disponível ou se o backup restaurado não for atual, recrie todas as entradas ausentes. Por exemplo, recrie todas as entradas ausentes de seus bancos de dados de usuários, dispositivos de backup, logons, pontos de extremidade, etc. do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A melhor maneira de recriar entradas é executar os scripts originais que as criaram.  
  
> [!IMPORTANT]  
>  É recomendável proteger os scripts para evitar que eles sejam alterados por indivíduos não autorizados.  
  
-   Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver configurada como um Distribuidor de replicação, você deverá restaurar o banco de dados de distribuição. Para obter mais informações, veja [Fazer backup e restaurar bancos de dados replicados](../replication/administration/back-up-and-restore-replicated-databases.md).  
  
-   Mova os bancos de dados do sistema para os locais que você registrou anteriormente. Para obter mais informações, veja [Mover bancos de dados do sistema](system-databases.md).  
  
-   Verifique se os valores da configuração de todo o servidor correspondem aos valores registrados anteriormente.  
  
##  <a name="Resource"></a> Recriar o banco de dados de recursos  
 O procedimento a seguir recria o banco de dados de recursos do sistema. Quando você recria o banco de dados de recursos, todos os service packs e hot fixes são perdidos, e portanto, devem ser reaplicados.  
  
#### <a name="to-rebuild-the-resource-system-database"></a>Para recriar o banco de dados do sistema de recursos:  
  
1.  Inicie o programa de Instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (setup.exe) da mídia de distribuição.  
  
2.  Na área de navegação à esquerda, clique em **Manutenção**e em **Reparar**.  
  
3.  A regra de suporte à Instalação e as rotinas de arquivos são executadas para garantir que o sistema tenha os pré-requisitos instalados e que o computador aprove as regras de validação da Instalação. Clique em **OK** ou em **Instalar** para continuar.  
  
4.  Na página Selecionar Instância, selecione a instância a ser reparada e, em seguida, clique em **Avançar**.  
  
5.  As regras de reparo são executadas para validar a operação. Para continuar, clique em **Avançar**.  
  
6.  Na página **Pronto para Reparar** , clique em **Reparar**. A página Concluído indica que a operação foi concluída.  
  
##  <a name="CreateMSDB"></a> Criar um novo banco de dados msdb  
 Se o `msdb` banco de dados está danificado e você não tiver um backup do `msdb` banco de dados, você pode criar uma nova `msdb` usando o **instmsdb** script.  
  
> [!WARNING]  
>  Recriar a `msdb` banco de dados usando o **instmsdb** script eliminará todas as informações armazenadas no `msdb` , como trabalhos, alerta, operadores, planos de manutenção, histórico de backup, as configurações de gerenciamento baseado em políticas , Banco de dados de email, Data Warehouse de desempenho, etc.  
  
1.  Pare todos os serviços que estejam se conectando ao [!INCLUDE[ssDE](../../includes/ssde-md.md)], inclusive o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, [!INCLUDE[ssRS](../../includes/ssrs.md)], [!INCLUDE[ssIS](../../includes/ssis-md.md)], e todos os aplicativos que estejam usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como um repositório de dados.  
  
2.  Inicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir da linha de comando usando o comando: `NET START MSSQLSERVER /T3608`  
  
     Para obter mais informações, veja [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
3.  Em outra janela de linha de comando, Desanexe o `msdb` banco de dados, executando o comando a seguir, substituindo  *\<servername >* com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: `SQLCMD -E -S<servername> -dmaster -Q"EXEC sp_detach_db msdb"`  
  
4.  Usando o Windows Explorer, renomeie o `msdb` arquivos de banco de dados. Por padrão, eles estão na subpasta DATA da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
5.  Usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, pare e reinicie o serviço [!INCLUDE[ssDE](../../includes/ssde-md.md)] normalmente.  
  
6.  Em uma janela de linha de comando, conecte-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e execute o comando: `SQLCMD -E -S<servername> -i"C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Install\instmsdb.sql" -o" C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Install\instmsdb.out"`  
  
     Substitua *\<servername>* pela instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Use o caminho do sistema de arquivo da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
7.  Usando o Bloco de Notas do Windows, abra o arquivo **instmsdb.out** e verifique se há erros na saída.  
  
8.  Aplique novamente pacotes de serviços ou o hotfix instalado na instância.  
  
9. Recrie o conteúdo de usuário armazenada em do `msdb` banco de dados, como trabalhos, alerta etc.  
  
10. Backup de `msdb` banco de dados.  
  
##  <a name="Troubleshoot"></a> Solução de problemas de erros de recriação  
 Erros de sintaxe e outros erros em tempo de execução são exibidos na janela do prompt de comando. Examine os erros de sintaxe a seguir na instrução da Instalação:  
  
-   Marca de barra (/) ausente na frente de cada nome de parâmetro.  
  
-   Sinal de igualdade (=) ausente entre o nome do parâmetro e o valor do parâmetro.  
  
-   Presença de espaços em branco entre o nome do parâmetro e o sinal de igual.  
  
-   Presença de vírgulas (,) ou outros caracteres que não são especificados na sintaxe.  
  
 Depois que a operação de recriação é concluída, examine se há erros nos logs do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O local do log padrão é C:\Arquivos de Programas\Microsoft SQL Server\120\Setup Bootstrap\Logs. Para localizar o arquivo de log que contém os resultados do processo de recriação, altere os diretórios para a pasta Logs em um prompt de comando e execute `findstr /s RebuildDatabase summary*.*`. Essa pesquisa apontará para qualquer arquivo de log que contenha os resultados da recriação dos bancos de dados do sistema. Abra os arquivos de log e examine-os para verificar se há mensagens de erro relevantes.  
  
## <a name="see-also"></a>Consulte também  
 [Bancos de dados do sistema](system-databases.md)  
  
  
