---
title: Restauração por etapas de bancos de dados com tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 732c9721-8dd4-481d-8ff9-1feaaa63f84f
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3c9ee00a81dd64ea1fa6093eaccc8d9b96e0aa59
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48170096"
---
# <a name="piecemeal-restore-of-databases-with-memory-optimized-tables"></a>Restauração por etapas de bancos de dados com tabelas com otimização de memória
  A restauração por etapas tem suporte em bancos de dados com tabelas com otimização de memória, exceto para uma restrição descrita abaixo. Para obter mais informações sobre backup e restauração por etapas, veja [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql) e [Restaurações por etapas &#40;SQL Server&#41;](../backup-restore/piecemeal-restores-sql-server.md).  
  
 Um grupo de arquivos com otimização de memória deve ser submetido a backup e restaurado junto com um grupo de arquivos primário:  
  
-   Se você submeter a backup (ou restaurar) o grupo de arquivos primário, especifique o grupo de arquivos com otimização de memória.  
  
-   Se você submeter a backup (ou restaurar) o grupo de arquivos com otimização de memória, especifique o grupo de arquivos primário.  
  
 Os principais cenários para backup e restauração por etapas são:  
  
-   O backup por etapas permite reduzir o tamanho do backup. Alguns exemplos:  
  
    -   Configurar o backup de banco de dados para ocorrer em horas ou dias diferentes para minimizar o impacto sobre a carga de trabalho. Um exemplo é um banco de dados muito grande (maior que 1 TB) em que um backup completo de banco de dados não pode ser concluído no tempo alocado para a manutenção do banco de dados. Nessa situação, você pode usar o backup por etapas para fazer backup do banco de dados inteiro em vários backup por etapas.  
  
    -   Se um grupo de arquivos for marcado como somente leitura, ele não exigirá um backup de log de transações após ser marcado como somente leitura. Você pode optar por fazer backup do grupo de arquivos apenas uma vez depois de marcá-lo como somente leitura.  
  
-   Restauração por etapas.  
  
    -   A meta de uma restauração por etapas é colocar as partes importantes do banco de dados online, sem esperar por todos os dados. Por exemplo, se um banco de dados tiver dados particionados, as partições mais antigas serão usadas apenas raramente. É possível restaurá-los somente conforme necessário. O mesmo ocorre com grupos de arquivos que contêm, por exemplo, dados históricos.  
  
    -   Usando o reparo de página, você pode corrigir danos de página, especificamente restaurando a página. Para obter mais informações, veja [Restaurar páginas &#40;SQL Server&#41;](../backup-restore/restore-pages-sql-server.md).  
  
## <a name="samples"></a>Exemplos  
 Os exemplos usam o seguinte esquema:  
  
```  
CREATE DATABASE imoltp  
ON PRIMARY (name = imoltp_primary1, filename = 'c:\data\imoltp_data1.mdf')  
LOG ON (name = imoltp_log, filename = 'c:\data\imoltp_log.ldf')  
GO  
  
ALTER DATABASE imoltp ADD FILE (name = imoltp_primary2, filename = 'c:\data\imoltp_data2.ndf')  
GO  
  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_secondary  
ALTER DATABASE imoltp ADD FILE (name = imoltp_secondary, filename = 'c:\data\imoltp_secondary.ndf') TO FILEGROUP imoltp_secondary  
GO  
  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA   
ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod   
ALTER DATABASE imoltp ADD FILE (name='imoltp_mod2', filename='c:\data\imoltp_mod2') TO FILEGROUP imoltp_mod   
GO  
```  
  
### <a name="backup"></a>Backup  
 Este exemplo mostra como fazer backup do grupo de arquivos primário e do grupo de arquivos com otimização de memória. Você deve especificar o grupo de arquivos primário e com otimização de memória.  
  
```  
backup database imoltp filegroup='primary', filegroup='imoltp_mod' to disk='c:\data\imoltp.dmp' with init  
```  
  
 O exemplo a seguir mostra que o backup de grupos de arquivos, que não sejam o grupo de arquivos primário e com otimização de memória, funciona de maneira semelhante para os bancos de dados sem tabelas com otimização de memória. O comando a seguir faz backup do grupo de arquivos secundário  
  
```  
backup database imoltp filegroup='imoltp_secondary' to disk='c:\data\imoltp_secondary.dmp' with init  
```  
  
### <a name="restore"></a>Restaurar  
 O exemplo a seguir mostra como restaurar o grupo de arquivos primário e o grupo de arquivos com otimização de memória juntos.  
  
```  
restore database imoltp filegroup = 'primary', filegroup = 'imoltp_mod'   
from disk='c:\data\imoltp.dmp' with partial, norecovery  
  
--restore the transaction log  
 RESTORE LOG [imoltp] FROM DISK = N'c:\data\imoltp_log.dmp' WITH  FILE = 1,  NOUNLOAD,  STATS = 10  
GO  
```  
  
 O próximo exemplo mostra que a restauração de grupos de arquivos, que não sejam o grupo de arquivos primário e com otimização de memória, funciona de maneira semelhante para os bancos de dados sem tabelas com otimização de memória.  
  
```  
RESTORE DATABASE [imoltp] FILE = N'imoltp_secondary'   
FROM  DISK = N'c:\data\imoltp_secondary.dmp' WITH  FILE = 1,  RECOVERY,  NOUNLOAD,  STATS = 10  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Backup, restauração e recuperação de tabelas com otimização de memória](../../database-engine/backup-restore-and-recovery-of-memory-optimized-tables.md)  
  
  
