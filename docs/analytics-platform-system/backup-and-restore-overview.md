---
title: Backup e restauração - Parallel Data Warehouse | Microsoft Docs
description: Descreve como os dados de backup e restauração funcionam para o Parallel Data Warehouse (PDW). Operações de backup e restauração são usadas para recuperação de desastres. Backup e restauração também podem ser usados para copiar um banco de dados de um dispositivo para outro dispositivo.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 01/19/2019
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0b95d18eb38bbe0012235304747ca80b3dc19a79
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200966"
---
# <a name="backup-and-restore"></a>Backup e restauração

Descreve como os dados de backup e restauração funcionam para o Parallel Data Warehouse (PDW). Operações de backup e restauração são usadas para recuperação de desastres. Backup e restauração também podem ser usados para copiar um banco de dados de um dispositivo para outro dispositivo.  
    
## <a name="BackupRestoreBasics"></a>Noções básicas sobre backup e restauração

Um PDW *backup do banco de dados* é uma cópia de um banco de dados do dispositivo, armazenado em um formato para que possa ser usado para restaurar o banco de dados original em um dispositivo.  
  
Um backup de banco de dados PDW é criado com o [BACKUP do banco de dados](../t-sql/statements/backup-database-parallel-data-warehouse.md) instrução t-sql e formatada para uso com o [RESTAURAR banco de dados](../t-sql/statements/restore-database-parallel-data-warehouse.md) instrução; não é utilizável para qualquer outra finalidade. O backup só pode ser restaurado em um dispositivo com o mesmo número ou um número maior de nós de computação.  
  
<!-- MISSING LINKS
The [master database](master-database.md) is a SMP SQL Server database. It is backed up with the BACKUP DATABASE statement. To restore master, use the [Restore the Master Database](configuration-manager-restore-master-database.md) page of the Configuration Manager tool.  
-->
  
PDW usa tecnologia de backup do SQL Server para fazer backup e restaurar bancos de dados do dispositivo. Opções de backup do SQL Server são pré-configurados para usar a compactação de backup. Não é possível definir as opções de backup, como compactação, soma de verificação, tamanho de bloco e contagem de buffer.  
  
Backups de banco de dados são armazenados em um ou mais servidores de backup, que existe em sua própria rede de cliente.  Grava um backup de banco de dados do usuário em paralelo diretamente de nós de computação em um servidor de backup e restaura um backup de banco de dados do usuário em paralelo diretamente do servidor de backup para os nós de computação do PDW.  
  
Backups são armazenados no servidor de backup como um conjunto de arquivos no sistema de arquivos do Windows. Um backup de banco de dados PDW só pode ser restaurado para o PDW. No entanto, você pode arquivar backups de banco de dados do servidor de backup para outro local, usando processos padrão da backup de arquivo do Windows. Para obter mais informações sobre servidores de backup, consulte [adquirir e configurar um servidor de backup](acquire-and-configure-backup-server.md).  
  
## <a name="BackupTypes"></a>Tipos de backup do banco de dados

Há dois tipos de dados que precisam de backup: bancos de dados de usuário e bancos de dados do sistema (por exemplo, o banco de dados mestre). PDW não fazer backup de log de transações.  
  
Um backup de banco de dados completo é um backup de um banco de dados inteiro do PDW. Isso é o tipo de backup padrão. Um backup completo de um banco de dados de usuário inclui usuários de banco de dados e funções de banco de dados. Um backup do mestre inclui logons.  
  
Um backup diferencial contém todas as alterações desde o último backup completo. Um backup diferencial geralmente leva menos tempo do que um backup completo e pode ser executado com mais frequência. Quando vários backups diferenciais se baseiam no mesmo backup completo, cada diferencial inclui todas as alterações no diferencial anterior.  
  
Por exemplo, você poderia criar um backup completo semanal e um backup diferencial diário. Para restaurar o banco de dados do usuário, o backup completo mais a última diferencial (se houver) precisa ser restaurado.  
  
Um backup diferencial só há suporte para bancos de dados do usuário. Um backup do mestre é sempre um backup completo.  
  
Para fazer backup de todo dispositivo, você precisará executar um backup de todos os bancos de dados de usuário e um backup do banco de dados mestre.  
  
## <a name="BackupProc"></a>Processo de backup do banco de dados

O diagrama a seguir mostra o fluxo de dados durante um backup de banco de dados.  
  
![O processo de backup PDW](media/backup-process.png "processo de backup do PDW")  
  
O processo de backup funciona da seguinte maneira:  
  
1.  O usuário envia uma instrução tsql de banco de dados de BACKUP para o nó de controle.  
  
    -   O backup é um backup completo ou diferencial.  
  
2.  Para bancos de dados do usuário, o nó de controle (mecanismo de MPP) cria um plano de consulta distribuída para executar um backup de banco de dados paralelo.  
  
3.  Cada nó envolvido nas cópias de backup, seu arquivo de backup para o servidor de backup usando a funcionalidade de backup do SQL Server.  
  
    -   Cada nó envolvido copia um arquivo de backup para o servidor de backup.  
  
    -   O backup do banco de dados de usuário (completo ou diferencial) inclui um backup da parte do banco de dados armazenado em cada nó de computação e um backup de banco de dados usuários e funções de banco de dados.  
  
4.  O dispositivo executará o backup em paralelo usando a rede InfiniBand.  
  
    -   PDW executa cada backup completo e diferencial em paralelo. No entanto, vários backups de banco de dados não são executados simultaneamente. Cada solicitação de backup deve aguardar backups enviados anteriormente ao fim.  
  
    -   Um backup do banco de dados mestre só faz backup dos dados do nó de controle. Esse tipo de backup é executado em série.  
  
5.  Um backup de banco de dados do PDW é um grupo de arquivos armazenados em um diretório que reside fora do dispositivo. O nome do diretório é especificado como um nome de caminho e o diretório de rede. O diretório não pode ser um caminho local e não pode ser no dispositivo.  
  
6.  Depois que o backup for concluído, você pode usar o sistema de arquivos do Windows para copiar o diretório de backup para outro local, se desejado.  
  
    -   Um backup somente pode ser restaurado para um dispositivo de PDW que tem um número igual ou maior de nós de computação.  
  
    -   Você não pode alterar o nome do backup antes de executar uma restauração. O nome do diretório de backup deve corresponder ao nome do nome original do backup. O nome original do backup está localizado no arquivo de backup dentro do diretório de backup. Para restaurar um banco de dados para um nome diferente, você pode especificar o novo nome no comando restore. Por exemplo: `RESTORE DATABASE MyDB1 FROM DISK = ꞌ\\10.192.10.10\backups\MyDB2ꞌ`.  
  
## <a name="RestoreModes"></a>Modos de restauração de banco de dados

Uma restauração de banco de dados completo recria o banco de dados do PDW, usando os dados no backup do banco de dados. A restauração de banco de dados é realizada pela primeira vez, restaurando um backup completo e, em seguida, opcionalmente, restaurando um backup diferencial. A restauração de banco de dados inclui os usuários de banco de dados e funções de banco de dados.  
  
Uma restauração somente de cabeçalho retorna as informações de cabeçalho para um banco de dados. Ele não restaura dados para o dispositivo.  
  
Uma restauração de dispositivo é uma restauração do dispositivo inteiro. Isso inclui a restauração de banco de dados mestre e de todos os bancos de dados do usuário.  
  
## <a name="RestoreProc"></a>Processo de restauração

O diagrama a seguir mostra o fluxo de dados durante uma restauração de banco de dados.  
  
![Processo de restauração](media/restore-process.png "processo de restauração")  
  
## <a name="restoring-to-an-appliance-with-the-same-number-of-compute-nodes"></a>Restaurando para um dispositivo com o mesmo número de nós de computação * *  
  
Ao restaurar os dados, o dispositivo detecta o número de nós de computação no dispositivo de origem e o dispositivo de destino. Se ambos os dispositivos têm um número igual de nós de computação, o processo de restauração funciona da seguinte maneira:  
  
1.  O backup do banco de dados a ser restaurado está disponível em um compartilhamento de arquivos do Windows em um servidor de backup não seja de dispositivo. Para obter melhor desempenho, esse servidor está conectado à rede InfiniBand appliance.  
  
2.  O usuário envia um [RESTAURAR banco de dados](../t-sql/statements/restore-database-parallel-data-warehouse.md) instrução tsql para o nó de controle.  
  
    -   A restauração é uma restauração completa ou uma restauração de cabeçalho. A restauração completa restaura um backup completo e, em seguida, opcionalmente, restaura um backup diferencial.  
  
3.  O nó de controle (mecanismo de MPP) cria um plano de consulta distribuída para executar uma restauração de banco de dados paralelo.  
  
    -   SQL ServerPDW executa a restauração de um banco de dados do usuário em paralelo. No entanto, vários backups de banco de dados e restaurações não são executadas simultaneamente. O mecanismo MPP coloca cada instrução restore dentro de uma fila; ele deve esperar para backup enviada anteriormente e restaurar as solicitações para concluir.  
  
    -   Uma restauração de banco de dados mestre só restaura os dados para o nó de controle; a restauração é executada em série.  
  
    -   Uma restauração das informações de cabeçalho é uma operação rápida e não restaura todos os dados para os nós de computação ou controle. Em vez disso, o nó de controle retorna os resultados como saída da consulta.  
  
4.  Os arquivos de backup copiados para os nós de computação corretos em paralelo, normalmente pela rede InfiniBand appliance.  
  
5.  Cada nó de computação restaura sua parte do banco de dados do usuário. Se qualquer uma das restaurações não concluída com êxito, todos os bancos de dados são removidos e a restauração for concluído com êxito.  
  
## <a name="restoring-to-an-appliance-with-a-larger-number-of-compute-nodes"></a>Restaurando para um dispositivo com um número maior de nós de Computação  
  
A restauração de um backup em um dispositivo com um número maior de nós de Computação aumenta o tamanho do banco de dados alocado proporcionalmente ao número de nós de Computação.  
  
Por exemplo, ao restaurar um banco de dados de 60 GB de um dispositivo de 2 nós (30 GB por nó) para um dispositivo de 6 nós, o SQL Server PDW cria um banco de dados de 180 GB (6 nós com 30 GB por nó) no dispositivo de 6 nós. SQL Server PDW inicialmente restaura o banco de dados para 2 nós para coincidir com a configuração de fonte e, em seguida, redistribui os dados para todos os 6 nós.  
  
Após a redistribuição, cada nó de computação conterá menos dados reais e mais espaço livre do que cada nó de computação no dispositivo de origem menor. Use o espaço adicional para adicionar mais dados ao banco de dados. Se o tamanho do banco de dados restaurado é maior do que você precisa, você pode usar [ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) para reduzir os tamanhos dos arquivos de banco de dados.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tarefa de restauração e backup|Descrição|  
|---------------------------|---------------|  
|Prepare um servidor como um servidor de backup.|[Adquirir e configurar um servidor de backup](acquire-and-configure-backup-server.md)|  
|Fazer backup de um banco de dados.|[BANCO DE DADOS DE BACKUP](../t-sql/statements/backup-database-parallel-data-warehouse.md)|  
|Restaure um banco de dados.|[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)|    

<!-- MISSING LINKS

|Create a disaster recovery plan.|[Create a Disaster Recovery Plan](create-disaster-recovery-plan.md)|
|Restore the master database.|To restore the master database, use the [Restore the master database](configuration-manager-restore-master-database.md) page in the Configuration Manager tool.| 
|Copy a database from one appliance to another appliance.|[Copy a PDW database to another appliance](copy-pdw-database-to-another-appliance.md).|  
|Monitor backups and restores.|[Monitor backups and restores](monitor-backup-and-restore.md)|  

-->
