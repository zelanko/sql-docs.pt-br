---
title: Compactação de backup (SQL Server) | Microsoft Docs
description: Saiba mais sobre a compactação de backups do SQL Server, incluindo restrições, compensações de desempenho, a configuração da compactação de backup e a taxa de compactação.
ms.custom: ''
ms.date: 07/08/2020
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], backup compression
- backup compression [SQL Server], about backup compression
- compression [SQL Server], backup compression
- backups [SQL Server], compression
- backing up [SQL Server], backup compression
- backup compression [SQL Server]
ms.assetid: 05bc9c4f-3947-4dd4-b823-db77519bd4d2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 56c2f2cadd998a6daba51b46e46e2c141e1f0f38
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810282"
---
# <a name="backup-compression-sql-server"></a>Compactação de backup (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve a compactação dos backups do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , incluindo restrições, compensação de desempenho de backups compactados, a configuração da compactação de backup e a taxa de compactação.  Há suporte para a compactação de backup nas edições [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]: Enterprise, Standard e Developer.  Todas as edições do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou posterior podem restaurar um backup compactado. 
 
  
##  <a name="benefits"></a><a name="Benefits"></a> Benefícios  
  
-   Como um backup compactado é menor do que um backup não compactado dos mesmos dados, a compactação de um backup normalmente requer menos operações de E/S do dispositivo e, portanto, normalmente aumenta significativamente a velocidade do backup.  
  
     Para obter mais informações, consulte [Impacto de desempenho dos backups compactados](#PerfImpact), posteriormente neste tópico.  
  
  
##  <a name="restrictions"></a><a name="Restrictions"></a> Restrições  
 As restrições a seguir aplicam-se aos backups compactados:  
  
-   Backups compactados e não compactados não podem coexistir em um conjunto de mídias.  
  
-   Porém, as versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não podem ler os backups compactados.  
  
-   Backups NT não podem compartilhar uma fita com backups compactados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  
##  <a name="performance-impact-of-compressing-backups"></a><a name="PerfImpact"></a> Impacto de desempenho dos backups compactados  
 Por padrão, a compactação aumenta consideravelmente o uso da CPU, e o consumo adicional da CPU por parte do processo de compactação pode afetar negativamente as operações simultâneas. Portanto, convém criar backups compactados de baixa prioridade em uma sessão cujo uso da CPU é limitado pelo[Resource Governor](../../relational-databases/resource-governor/resource-governor.md). Para obter mais informações, consulte [Usar o Resource Governor para limitar o uso de CPU por meio de compactação de backup &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md).  
  
 Para obter uma boa visão do desempenho de E/S do seu backup, é possível isolar o E/S do backup para ou dos dispositivos avaliando as seguintes classificações dos contadores de desempenho:  
  
-   Contadores de desempenho de E/S do Windows, como os contadores de disco físico  
  
-   O contador de **Taxa de Transferência do Dispositivo em Bytes/s** do objeto [SQLServer:Backup Device](../../relational-databases/performance-monitor/sql-server-backup-device-object.md)  
  
-   O contador **Taxa de Transferência de Backup/Restauração/s** do objeto [SQLServer:Databases](../../relational-databases/performance-monitor/sql-server-databases-object.md)  
  
 Para obter informações sobre contadores do Windows, consulte a ajuda do Windows. Para obter informações sobre como trabalhar com contadores SQL Server, consulte [Usar objetos do SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md).  
  
   
##  <a name="calculate-the-compression-ratio-of-a-compressed-backup"></a><a name="CompressionRatio"></a> Calcular a taxa de compactação de um backup compactado  
 Para calcular a taxa de compactação de um backup, use os valores para o backup nas colunas **backup_size** e **compressed_backup_size** da tabela de histórico [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) da seguinte maneira:  
  
 **backup_size**:**compressed_backup_size**  
  
 Por exemplo, uma taxa de compactação de 3:1 indica que você está economizando aproximadamente 66% de espaço em disco. Para consultar essas colunas, você pode usar a seguinte instrução Transact-SQL:  
  
```sql  
SELECT backup_size/compressed_backup_size FROM msdb..backupset;  
```  
  
 A taxa de compactação de um backup compactado depende dos dados que foram compactados. Uma variedade de fatores pode impactar na taxa de compactação obtida. Os principais fatores incluem:  
  
-   O tipo de dados.  
  
     Os dados de caractere compactam mais do que outros tipos de dados.  
  
-   A consistência dos dados entre as linhas em uma página.  
  
     Normalmente, se uma página contém várias linhas com um campo contendo o mesmo valor, poderá ocorrer uma compactação significativa para esse valor. Por outro lado, para um banco de dados que contém dados aleatórios ou contém somente uma grande linha por página, um backup compactado pode ser tão grande quanto um backup não compactado.  
  
-   Se os dados são criptografados  
  
     A compactação de dados criptografados é significativamente menor do que a compactação de dados equivalentes não criptografados. Por exemplo, se os dados forem criptografados no nível da coluna com Always Encrypted ou com outra criptografia no nível do aplicativo, a compactação dos backups poderá não reduzir significativamente o tamanho.

     Para obter mais informações relacionadas à compactação de bancos de dados criptografados com a tecnologia TDE (Transparent Data Encryption), confira a [Compactação de backup com TDE](#backup-compression-with-tde).

-   Se o banco de dados é compactado.  
  
     Se o banco de dados for compactado, a compactação de backups poderá não reduzir muito o seu tamanho.  

## <a name="backup-compression-with-tde"></a>Compactação de backup com TDE

Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], definir `MAXTRANSFERSIZE` **maior que 65.536 (64 KB)** permite um algoritmo de compactação otimizada para bancos de dados criptografados com [TDE (Transparent Data Encryption)](../../relational-databases/security/encryption/transparent-data-encryption.md) que primeiro descriptografa uma página, compacta-a e, depois, criptografa-a novamente. Se `MAXTRANSFERSIZE` não for especificado ou se `MAXTRANSFERSIZE = 65536` (64 KB) for usado, a compactação de backup com bancos de dados criptografados com TDE compactará diretamente as páginas criptografadas e poderá não resultar em taxas de compactação satisfatórias. Para obter mais informações, consulte [Compactação de backup para bancos de dados habilitados para TDE](/archive/blogs/sqlcat/sqlsweet16-episode-1-backup-compression-for-tde-enabled-databases).

Do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CU5 em diante, a configuração de `MAXTRANSFERSIZE` não é mais necessária para habilitar esse algoritmo de compactação otimizado com TDE. Se o comando backup for especificado `WITH COMPRESSION` ou a configuração de servidor *padrão de compactação de backup* for definido como 1, `MAXTRANSFERSIZE` será automaticamente aumentado para 128 K para habilitar o algoritmo otimizado. Se `MAXTRANSFERSIZE` for especificado no comando de backup com um valor > 64 K, o valor fornecido será respeitado. Em outras palavras, o SQL Server nunca diminuirá o valor automaticamente, ele somente o aumentará. Se você precisar fazer backup de um banco de dados criptografado com TDE com `MAXTRANSFERSIZE = 65536`, será preciso especificar `WITH NO_COMPRESSION` ou garantir que a configuração de servidor *padrão de compactação de backup* seja definida como 0.

Para obter mais informações, confira [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md).

##  <a name="allocation-of-space-for-the-backup-file"></a><a name="Allocation"></a> Alocação de espaço para o arquivo de backup  
 Para backups compactados, o tamanho do arquivo de backup final depende de como os dados são compactáveis e isto é desconhecido antes da conclusão da operação de backup.  Portanto, por padrão, ao fazer backup de um banco de dados usando compactação, o Mecanismo de Banco de Dados usa um algoritmo de pré-alocação para o arquivo de backup. Este algoritmo pré-aloca um percentual predefinido do tamanho do banco de dados para o arquivo de backup. Se for necessário mais espaço durante a operação de backup, o Mecanismo de Banco de Dados crescerá o arquivo. Se o tamanho final for menor que o espaço alocado, no final da operação de backup, o Mecanismo de Banco de Dados reduzirá o arquivo para o tamanho final real do backup.  
  
 Para permitir que o arquivo de backup somente cresça conforme o necessário para alcançar seu tamanho final, use o sinalizador de rastreamento 3042. O sinalizador de rastreamento 3042 faz a operação de backup ignorar o algoritmo padrão de pré-alocação da compactação de backup. Este sinalizador de rastreamento será útil se você precisar salvar em espaço alocando somente o tamanho real necessário para o backup compactado. Porém, usar este sinalizador de rastreamento pode causar uma pequena penalidade de desempenho (um possível aumento na duração da operação de backup).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Configurar compactação de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/configure-backup-compression-sql-server.md)  
  
-   [Exibir ou configurar a opção de configuração de servidor backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
-   [Usar o Resource Governor para limitar o uso de CPU por meio de compactação de backup &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [DBCC TRACEON &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
  
-   [DBCC TRACEOFF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
  
