---
title: "Fazendo backup de um banco de dados com tabelas com otimiza&#231;&#227;o de mem&#243;ria | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 83d47694-e56d-4dae-b54e-14945bf8ba31
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# Fazendo backup de um banco de dados com tabelas com otimiza&#231;&#227;o de mem&#243;ria
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  As tabelas com otimização de memória são incluídas no backup como parte de backups regulares de banco de dados. Quanto às tabelas baseadas em disco, o CHECKSUM de dados e os pares de arquivos delta são validados como parte do backup de banco de dados para detectar corrupção do armazenamento.  
  
> [!NOTE]  
>  Durante um backup, se você detectar um erro de CHECKSUM em um ou mais arquivos em um grupo de arquivos com otimização de memória, a operação de backup falhará. Nessa situação, você deve restaurar seu banco de dados do último backup válido.  
>   
>  Se você não tiver um backup, poderá exportar os dados das tabelas com otimização de memória e as tabelas baseadas em disco e recarregá-las depois que você remover e recriar o banco de dados.  
  
 Um backup completo de um banco de dados com uma ou mais tabelas com otimização de memória consiste no armazenamento alocado para tabelas baseadas em disco (se houver), no log de transações ativas e nos pares de arquivos de dados e delta (também conhecidos como pares de arquivos de ponto de verificação) para tabelas otimizadas para memória. No entanto, como descrito em [Durabilidade de tabelas com otimização de memória](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md), o armazenamento usado por tabelas com otimização de memória pode ser muito maior do que seu tamanho em memória, e afeta o tamanho do backup do banco de dados.  
  
## Backup de banco de dados Completo  
 Esta discussão se concentra em backups de banco de dados para bancos de dados que têm apenas tabelas com otimização de memória, uma vez que o backup de tabelas baseadas em disco é igual. Os pares do arquivos de ponto de verificação no grupo de arquivos com otimização de memória poderia estar em diversos estados. A tabela a seguir descreve qual parte dos arquivos é inserida no backup.  
  
|Estado do par de arquivos de ponto de verificação|Backup|  
|--------------------------------|------------|  
|PRECREATED|Somente metadados de arquivo|  
|UNDER CONSTRUCTION|Somente metadados de arquivo|  
|ACTIVE|Metadados de arquivo mais bytes usados|  
|MERGE TARGET|Somente metadados de arquivo|  
|AGUARDANDO O TRUNCAMENTO DE LOG|Metadados de arquivo mais bytes usados|  
  
 Para obter descrições dos estados de pares de arquivos de ponto de verificação, veja [sys.dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) e sua coluna state_desc.  
  
 O tamanho dos backups de banco de dados com uma ou mais tabelas com otimização de memória normalmente é maior do que o tamanho em memória mas menor do que o do armazenamento em disco. O tamanho extra depende do número de linhas excluídas, entre outros fatores.  
  
### Estimando o tamanho do backup de banco de dados completo  
  
> [!IMPORTANT]  
>  É recomendável que você não use o valor de BackupSizeInBytes para estimar o tamanho do backup para O OLTP na Memória.  
  
 O primeiro cenário de carga de trabalho é para (principalmente) inserir. Neste cenário, a maioria dos arquivos de dados estará no estado Ativo, totalmente carregados e com muito poucas linhas excluídas. O tamanho do backup do banco de dados está próximo do tamanho dos dados na memória.  
  
 É o segundo cenário de carga de trabalho para operações de atualização, exclusão e inserção frequentes. Na pior das hipóteses, cada um dos pares de arquivos de ponto de verificação será 50% carregado, após a contagem das linhas excluídas. O tamanho do backup de banco de dados terá pelo menos 2 vezes o tamanho dos dados na memória.  
  
## Backups diferenciais de bancos de dados com tabelas com otimização de memória  
 O armazenamento de tabelas com otimização de memória consiste em dados e arquivos delta, conforme descrito em [Durabilidade de tabelas com otimização de memória](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md). O backup diferencial de um banco de dados com tabelas com otimização de memória contém os seguintes dados:  
  
-   O backup diferencial para grupos de arquivos que armazenam tabelas baseadas em disco não é afetado pela presença de tabelas com otimização de memória.  
  
-   O log de transações ativas é igual ao de um backup total do banco de dados.  
  
-   Para um grupo de arquivos de dados com otimização de memória, o backup diferencial usa o mesmo algoritmo que o backup total do banco de dados para identificar os arquivos de dados e delta para o backup, mas depois ele filtra o subconjunto de arquivos da seguinte maneira:  
  
    -   Um arquivo de dados contém linhas recém-inseridas e, quando está cheio, ele é fechado e marcado como somente leitura. Um arquivo de dados será armazenado em backup apenas se ele tiver sido fechado após o último backup completo do banco de dados. O backup diferencial só faz backup de arquivos de dados que contém as linhas inseridas desde o último backup completo do banco de dados. Uma exceção é um cenário de atualização e de exclusão onde é possível que algumas das linhas inseridas talvez já tenham sido ou marcadas para coleta de lixo ou já coletadas como lixo.  
  
    -   Um arquivo delta armazena referências às linhas de dados excluídas. Como qualquer transação futura pode excluir uma linha, um arquivo delta pode ser modificado a qualquer momento em seu tempo de vida, pois ele nunca é fechado. Um arquivo delta é sempre armazenado em backup. Os arquivos delta costumam usam menos de 10% do armazenamento; portanto, os arquivos delta têm um impacto mínimo sobre o tamanho do backup diferencial.  
  
 Se as tabelas com otimização de memória forem uma parte significativa do tamanho do banco de dados, o backup diferencial poderá reduzir significativamente o tamanho do backup do banco de dados. Para cargas de trabalho típicas de OLTP, os backups diferenciais serão significativamente menores do que os backups completos de banco de dados.  
  
## Consulte também  
 [Backup, restauração e recuperação de tabelas com otimização de memória](../Topic/Backup,%20Restore,%20and%20Recovery%20of%20Memory-Optimized%20Tables.md)  
  
  