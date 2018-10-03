---
title: Fazendo backup de um banco de dados com tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 83d47694-e56d-4dae-b54e-14945bf8ba31
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4b791f83342d02fb003a14f48861ae992ddc37df
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48190286"
---
# <a name="backing-up-a-database-with-memory-optimized-tables"></a>Fazendo backup de um banco de dados com tabelas com otimização de memória
  As tabelas com otimização de memória são incluídas no backup como parte de backups regulares de banco de dados. Quanto às tabelas baseadas em disco, o CHECKSUM de dados e os pares de arquivos delta são validados como parte do backup de banco de dados para detectar corrupção do armazenamento.  
  
> [!NOTE]  
>  Durante um backup, se você detectar um erro de CHECKSUM em um ou mais arquivos em um grupo de arquivos com otimização de memória, você não poderá restaurar e reiniciar o banco de dados. Nessa situação, você deve restaurar seu banco de dados com o último backup válido. Se você não tiver um backup, poderá exportar os dados das tabelas com otimização de memória e as tabelas baseadas em disco e recarregá-las depois que você remover e recriar o banco de dados.  
  
 Um backup completo de um banco de dados com uma ou mais tabelas com otimização de memória consiste no armazenamento alocado para tabelas baseadas em disco (se houver), no log de transações ativas e nos pares de arquivos de dados e delta (também conhecidos como pares de arquivos de ponto de verificação) para tabelas otimizadas para memória. No entanto, como descrito em [Durabilidade de tabelas com otimização de memória](memory-optimized-tables.md), o armazenamento usado por tabelas com otimização de memória pode ser muito maior do que seu tamanho em memória, e afeta o tamanho do backup do banco de dados.  
  
## <a name="full-database-backup"></a>Backup de banco de dados Completo  
 Esta discussão se concentrará em backups de banco de dados para bancos de dados que têm apenas tabelas com otimização de memória, uma vez que o backup de tabelas baseadas em disco é igual. Os pares do arquivos de ponto de verificação no grupo de arquivos com otimização de memória poderia estar em diversos estados. A tabela a seguir descreve qual parte dos arquivos é inserida no backup.  
  
|Estado do par de arquivos de ponto de verificação|Backup|  
|--------------------------------|------------|  
|PRECREATED|Somente metadados de arquivo|  
|UNDER CONSTRUCTION|Somente metadados de arquivo|  
|Ativa|Metadados de arquivo mais bytes usados|  
|Origem mesclada|Metadados de arquivo mais bytes usados|  
|Destino de mesclagem|Somente metadados de arquivo|  
|REQUIRED FOR BACKUP/HA|Metadados de arquivo mais bytes usados|  
|IN TRANSITION TO TOMBSTONE|Somente metadados de arquivo|  
|TOMBSTONE|Somente metadados de arquivo|  
  
 O tamanho dos backups de banco de dados com uma ou mais tabelas com otimização de memória normalmente é maior do que o tamanho em memória mas menor do que o do armazenamento em disco. O tamanho adicional dependerá do número de linhas excluídas e do número de pares de arquivo de ponto de verificação nos estados Origem de mesclagem e REQUIRED FOR BACKUP/HA, que dependem indiretamente da carga de trabalho. Para obter descrições dos Estados para pares de arquivos de ponto de verificação, consulte [DM db_xtp_checkpoint_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql).  
  
### <a name="estimating-size-of-full-database-backup"></a>Estimando o tamanho do backup de banco de dados completo  
  
> [!IMPORTANT]  
>  É recomendável que você não use o valor de BackupSizeInBytes para estimar o tamanho do backup para O OLTP na Memória.  
  
 O primeiro cenário de carga de trabalho é para (principalmente) inserir. Neste cenário, a maioria dos arquivos de dados estará no estado Ativo, totalmente carregados e com muito poucas linhas excluídas. O tamanho do backup do banco de dados estará próximo do tamanho dos dados na memória.  
  
 O segundo cenário de carga de trabalho é para operações frequentes de inserção, exclusão e atualização: no pior caso, cada um dos pares de arquivos de ponto de verificação será 50% carregado, após a contabilidade das linhas excluídas. Dessa forma, o tamanho do backup de banco de dados terá pelo menos 2 vezes o tamanho dos dados na memória. Além disso, alguns pares de arquivos de ponto de verificação nos estados Origem de mesclagem e Necessário para backup/alta disponibilidade se somarão ao tamanho do backup de banco de dados.  
  
## <a name="differential-backups-of-databases-with-memory-optimized-tables"></a>Backups diferenciais de bancos de dados com tabelas com otimização de memória  
 O armazenamento de tabelas com otimização de memória consiste em dados e arquivos delta, conforme descrito em [Durabilidade de tabelas com otimização de memória](memory-optimized-tables.md). O backup diferencial de um banco de dados com tabelas com otimização de memória contém os seguintes dados:  
  
-   O backup diferencial para grupos de arquivos que armazenam tabelas baseadas em disco não é afetado pela presença de tabelas com otimização de memória.  
  
-   O log de transações ativas é igual ao de um backup total do banco de dados.  
  
-   Para um grupo de arquivos de dados com otimização de memória, o backup diferencial usa o mesmo algoritmo que o backup total do banco de dados para identificar os arquivos de dados e delta para o backup, mas depois ele filtra o subconjunto de arquivos da seguinte maneira:  
  
    -   Um arquivo de dados contém linhas recém-inseridas e, quando está cheio, ele é fechado e marcado como somente leitura. Um arquivo de dados será armazenado em backup apenas se ele tiver sido fechado após o último backup completo do banco de dados. O backup diferencial só realiza o backup de arquivos de dados que contêm as linhas inseridas desde o último backup completo do banco de dados, com exceção de um cenário de atualização e exclusão onde é possível que algumas das linhas inseridas já tenham sido marcadas para coleta de lixo ou já tenham sido limpas pelo coletor de lixo.  
  
    -   Um arquivo delta armazena referências às linhas de dados excluídas. Como qualquer transação futura pode excluir uma linha, um arquivo delta pode ser modificado a qualquer momento em seu tempo de vida, pois ele nunca é fechado. Um arquivo delta é sempre armazenado em backup. Os arquivos delta costumam usam menos de 10% do armazenamento; portanto, os arquivos delta têm um impacto mínimo sobre o tamanho do backup diferencial.  
  
 Se as tabelas com otimização de memória forem uma parte significativa do tamanho do banco de dados, o backup diferencial poderá reduzir significativamente o tamanho do backup do banco de dados.  
  
 Para cargas de trabalho típicas de OLTP, os backups diferenciais serão significativamente menores do que os backups completos de banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Backup, restauração e recuperação de tabelas com otimização de memória](restore-and-recovery-of-memory-optimized-tables.md)  
  
  
