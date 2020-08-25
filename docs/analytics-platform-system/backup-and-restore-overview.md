---
title: Backup e restauração
description: Descreve como o backup e a restauração de dados funcionam para o PDW (data warehouse paralelo). As operações de backup e restauração são usadas para recuperação de desastre. O backup e a restauração também podem ser usados para copiar um banco de dados de um dispositivo para outro dispositivo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 01/19/2019
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e7f106e462d3d1bb7848b15523ef3d3f7feed2a1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767205"
---
# <a name="backup-and-restore"></a>Backup e restauração

Descreve como o backup e a restauração de dados funcionam para o PDW (data warehouse paralelo). As operações de backup e restauração são usadas para recuperação de desastre. O backup e a restauração também podem ser usados para copiar um banco de dados de um dispositivo para outro dispositivo.  
    
## <a name="backup-and-restore-basics"></a><a name="BackupRestoreBasics"></a>Noções básicas de backup e restauração

Um *backup de banco de dados* PDW é uma cópia de um banco de dados de dispositivo, armazenado em um formato para que possa ser usado para restaurar o banco de dados original para um dispositivo.  
  
Um backup de banco de dados do PDW é criado com a instrução t-SQL do [banco de dados de backup](../t-sql/statements/backup-transact-sql.md?view=aps-pdw-2016) e formatado para uso com a instrução [Restore Database](../t-sql/statements/restore-statements-transact-sql.md?view=aps-pdw-2016) ; Ele não pode ser usado para nenhuma outra finalidade. O backup só pode ser restaurado para um dispositivo com o mesmo número ou um número maior de nós de computação.  
  
<!-- MISSING LINKS
The [master database](master-database.md) is a SMP SQL Server database. It is backed up with the BACKUP DATABASE statement. To restore master, use the [Restore the Master Database](configuration-manager-restore-master-database.md) page of the Configuration Manager tool.  
-->
  
O PDW usa SQL Server tecnologia de backup para backup e restauração de bancos de dados de dispositivo. SQL Server opções de backup são pré-configuradas para usar a compactação de backup. Não é possível definir as opções de backup, como compactação, soma de verificação, tamanho de bloco e contagem de buffer.  
  
Os backups de banco de dados são armazenados em um ou mais servidores de backup, que existem em sua própria rede de clientes.  O PDW grava um backup de banco de dados de usuário em paralelo diretamente dos nós de computação em um servidor de backup e restaura um backup de banco de dados de usuário em paralelo diretamente do servidor de backup para os nós de computação.  
  
Os backups são armazenados no servidor de backup como um conjunto de arquivos no sistema de arquivos do Windows. Um backup de banco de dados PDW só pode ser restaurado para o PDW. No entanto, você pode arquivar backups de banco de dados do servidor de backup para outro local usando processos padrão de backup de arquivos do Windows. Para obter mais informações sobre servidores de backup, consulte [adquirir e configurar um servidor de backup](acquire-and-configure-backup-server.md).  
  
## <a name="database-backup-types"></a><a name="BackupTypes"></a>Tipos de backup de banco de dados

Há dois tipos de dados que exigem um backup: bancos de dados de usuário e de sistema (como o banco de dados mestre). O PDW não faz backup do log de transações.  
  
Um backup de banco de dados completo é um backup de um banco de dados do PDW inteiro. Esse é o tipo de backup padrão. Um backup completo de um banco de dados de usuário inclui usuários de banco de dados e funções de banco de dados. Um backup do mestre inclui logons.  
  
Um backup diferencial contém todas as alterações desde o último backup completo. Um backup diferencial geralmente leva menos tempo do que um backup completo e pode ser executado com mais frequência. Quando vários backups diferenciais são baseados no mesmo backup completo, cada diferencial inclui todas as alterações no diferencial anterior.  
  
Por exemplo, você pode criar um backup completo semanalmente e um backup diferencial diariamente. Para restaurar o banco de dados do usuário, o backup completo mais a última diferencial (se houver) precisa ser restaurado.  
  
Um backup diferencial só tem suporte para bancos de dados de usuário. Um backup do mestre é sempre um backup completo.  
  
Para fazer backup de todo o dispositivo, você precisa executar um backup de todos os bancos de dados de usuário e um backup do banco de dados mestre.  
  
## <a name="database-backup-process"></a><a name="BackupProc"></a>Processo de backup do banco de dados

O diagrama a seguir mostra o fluxo de dados durante um backup de banco de dado.  
  
![Processo de backup do PDW](media/backup-process.png "Processo de backup do PDW")  
  
O processo de backup funciona da seguinte maneira:  
  
1.  O usuário envia uma instrução TSQL de banco de dados de BACKUP para o nó de controle.  
  
    -   O backup é um backup completo ou diferencial.  
  
2.  Para bancos de dados de usuário, o nó de controle (mecanismo MPP) cria um plano de consulta distribuído para executar um backup de banco de dados paralelo.  
  
3.  Cada nó envolvido no backup copia seu arquivo de backup para o servidor de backup usando SQL Server funcionalidade de backup.  
  
    -   Cada nó envolvido copia um arquivo de backup para o servidor de backup.  
  
    -   O backup do banco de dados do usuário (completo ou diferencial) inclui um backup da parte do banco de dados armazenado em cada nó de computação e um backup dos usuários do banco de dados e das funções de banco de dados.  
  
4.  O dispositivo executa o backup em paralelo usando a rede InfiniBand.  
  
    -   O PDW executa cada backup completo e diferencial em paralelo. No entanto, vários backups de banco de dados não são executados simultaneamente. Cada solicitação de backup deve aguardar até que os backups enviados anteriormente sejam concluídos.  
  
    -   Um backup do banco de dados mestre faz backup apenas dos dados do nó de controle. Esse tipo de backup é executado em série.  
  
5.  Um backup de banco de dados do PDW é um grupo de arquivos armazenados em um diretório que reside no dispositivo. O nome do diretório é especificado como um caminho de rede e um nome de diretório. O diretório não pode ser um caminho local e não pode estar no dispositivo.  
  
6.  Depois que o backup for concluído, você poderá usar o sistema de arquivos do Windows para copiar o diretório de backup para outro local, se desejar.  
  
    -   Um backup só pode ser restaurado para um dispositivo PDW que tenha um número igual ou maior de nós de computação.  
  
    -   Você não pode alterar o nome do backup antes de executar uma restauração. O nome do diretório de backup deve corresponder ao nome do nome original do backup. O nome original do backup está localizado no arquivo de backup.xml dentro do diretório de backup. Para restaurar um banco de dados para um nome diferente, você pode especificar o novo nome no comando Restore. Por exemplo: `RESTORE DATABASE MyDB1 FROM DISK = ꞌ\\10.192.10.10\backups\MyDB2ꞌ`.  
  
## <a name="database-restore-modes"></a><a name="RestoreModes"></a>Modos de restauração de banco de dados

Uma restauração de banco de dados completa recria o banco de dados do PDW usando o backup de banco de dado. A restauração do banco de dados é executada primeiro restaurando um backup completo e, opcionalmente, restaurando um backup diferencial. A restauração do banco de dados inclui os usuários do banco de dados e funções de banco de dados  
  
Uma restauração somente de cabeçalho retorna as informações de cabeçalho de um banco de dados. Ele não restaura dados para o dispositivo.  
  
Uma restauração de dispositivo é uma restauração de todo o dispositivo. Isso inclui a restauração de todos os bancos de dados de usuários e do mestre.  
  
## <a name="restore-process"></a><a name="RestoreProc"></a>Processo de restauração

O diagrama a seguir mostra o fluxo de dados durante uma restauração de banco de dado.  
  
![Processo de restauração](media/restore-process.png "Processo de restauração")  
  
## <a name="restoring-to-an-appliance-with-the-same-number-of-compute-nodes"></a>Restaurando para um dispositivo com o mesmo número de nós de computação * *  
  
Ao restaurar dados, o dispositivo detecta o número de nós de computação no dispositivo de origem e no dispositivo de destino. Se ambos os dispositivos tiverem um número igual de nós de computação, o processo de restauração funcionará da seguinte maneira:  
  
1.  O backup do banco de dados a ser restaurado está disponível em um compartilhamento de arquivos do Windows em um servidor de backup que não seja de dispositivo. Para obter o melhor desempenho, esse servidor está conectado à rede InfiniBand do dispositivo.  
  
2.  O usuário envia uma instrução TSQL do [banco de dados de restauração](../t-sql/statements/restore-statements-transact-sql.md?view=aps-pdw-2016) para o nó de controle.  
  
    -   A restauração é uma restauração completa ou uma restauração de cabeçalho. A restauração completa restaura um backup completo e, opcionalmente, restaura um backup diferencial.  
  
3.  O nó de controle (mecanismo MPP) cria um plano de consulta distribuído para executar uma restauração de banco de dados paralela.  
  
    -   O SQL ServerPDW executa a restauração de um banco de dados de usuário em paralelo. No entanto, vários backups e restaurações de banco de dados não são executados simultaneamente. O mecanismo MPP coloca cada instrução RESTORE em uma fila; Ele deve aguardar até que as solicitações de backup e restauração previamente enviadas sejam concluídas.  
  
    -   Uma restauração do banco de dados mestre restaura apenas os dados para o nó de controle; a restauração é executada em série.  
  
    -   Uma restauração das informações de cabeçalho é uma operação rápida e não restaura dados para os nós de computação ou de controle. Em vez disso, o nó de controle retorna os resultados como saída da consulta.  
  
4.  Os arquivos de backup são copiados para os nós de computação corretos em paralelo, geralmente pela rede InfiniBand do dispositivo.  
  
5.  Cada nó de computação restaura sua parte do banco de dados do usuário. Se qualquer uma das restaurações não for concluída com êxito, todos os bancos de dados serão removidos e a restauração será concluída sem êxito.  
  
## <a name="restoring-to-an-appliance-with-a-larger-number-of-compute-nodes"></a>Restaurando para um dispositivo com um número maior de nós de Computação  
  
A restauração de um backup em um dispositivo com um número maior de nós de Computação aumenta o tamanho do banco de dados alocado proporcionalmente ao número de nós de Computação.  
  
Por exemplo, ao restaurar um banco de dados de 60 GB de um dispositivo de 2 nós (30 GB por nó) para um dispositivo de 6 nós, SQL Server PDW cria um banco de dados de 180 GB (6 nós com 30 GB por nó) no dispositivo de 6 nós. O SQL Server PDW restaura inicialmente o banco de dados para dois nós a fim de corresponder à configuração de origem e, em seguida, redistribua-os para todos os 6 nós.  
  
Após a redistribuição, cada nó de computação conterá menos dados reais e mais espaço livre do que cada nó de computação no dispositivo de origem menor. Use o espaço adicional para adicionar mais dados ao banco de dados. Se o tamanho do banco de dados restaurado for maior do que o necessário, você poderá usar [ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) para reduzir os tamanhos do arquivo de banco de dados.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tarefa de backup e restauração|Descrição|  
|---------------------------|---------------|  
|Prepare um servidor como um servidor de backup.|[Adquirir e configurar um servidor de backup](acquire-and-configure-backup-server.md)|  
|Fazer backup de um banco de dados.|[BACKUP DATABASE](../t-sql/statements/backup-transact-sql.md?view=aps-pdw-2016)|  
|Restaurar um banco de dados.|[RESTAURAR BANCO DE DADOS](../t-sql/statements/restore-statements-transact-sql.md?view=aps-pdw-2016)|    

<!-- MISSING LINKS

|Create a disaster recovery plan.|[Create a Disaster Recovery Plan](create-disaster-recovery-plan.md)|
|Restore the master database.|To restore the master database, use the [Restore the master database](configuration-manager-restore-master-database.md) page in the Configuration Manager tool.| 
|Copy a database from one appliance to another appliance.|[Copy a PDW database to another appliance](copy-pdw-database-to-another-appliance.md).|  
|Monitor backups and restores.|[Monitor backups and restores](monitor-backup-and-restore.md)|  

-->
