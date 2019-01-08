---
title: Gerenciar o tamanho do arquivo de log de transações | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], size management
ms.assetid: 3a70e606-303f-47a8-96d4-2456a18d4297
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b2ebcd653adebed5541b1d2cdf814f638d0af683
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52816608"
---
# <a name="manage-the-size-of-the-transaction-log-file"></a>Gerenciar o tamanho do arquivo de log de transações
  Em alguns casos, pode ser útil reduzir ou expandir fisicamente o arquivo de log físico do log de transações de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Este tópico contém informações sobre como monitorar o tamanho de um log de transações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , reduzir o log de transações, adicionar ou aumentar um arquivo de log de transações, otimizar a taxa de crescimento do log de transações **tempdb** e controlar o crescimento de um arquivo de log de transações.  
  
  
##  <a name="MonitorSpaceUse"></a> Monitorar o uso do espaço em Log  
 Você pode monitorar o uso do espaço de log usando DBCC SQLPERF (LOGSPACE). Esse comando retorna informações sobre a quantidade de espaço de log usada atualmente e indica quando o log de transações precisa ser truncado. Para obter mais informações, veja [DBCC SQLPERF &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-sqlperf-transact-sql). Para obter informações sobre o tamanho atual de um arquivo de log, seu tamanho máximo e a opção de crescimento automático para o arquivo, você também pode usar as colunas **size**, **max_size** e **growth** para esse arquivo de log em **sys.database_files**. Para obter mais informações, consulte [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql).  
  
> [!IMPORTANT]  
>  Recomendamos que seja evitada a sobrecarga do disco de log.  
  
  
##  <a name="ShrinkSize"></a> Reduzir o tamanho do arquivo de Log  
 Para reduzir o tamanho físico de um arquivo de log físico, você deve reduzir o arquivo de log. Isso será útil se você souber que um arquivo de log de transações contém espaço não utilizado que você não precisará. A redução de um arquivo de log poderá ocorrer apenas enquanto o banco de dados estiver online e, pelo menos, enquanto um arquivo de log virtual estiver livre. Em alguns casos, talvez não seja possível reduzir o log antes do próximo truncamento de log.  
  
> [!NOTE]  
>  Fatores como uma transação demorada que mantêm arquivos de log virtuais ativos por um período extenso podem restringir a redução de log ou até mesmo impedir que o log seja reduzido. Para ver informações sobre os fatores que podem adiar o truncamento de log, consulte [O log de transações &#40;SQL Server&#41;](the-transaction-log-sql-server.md).  
  
 A redução de um arquivo de log remove um mais arquivos de log virtuais que não retêm nenhuma parte do log lógico (ou seja, *arquivos de log virtuais inativos*). Quando um arquivo de log de transações é reduzido, um número suficiente de arquivos de log virtuais inativos é removido do final do arquivo de log para reduzir o log aproximadamente ao tamanho do destino.  
  
 **Para reduzir um arquivo de log (sem reduzir os arquivos de banco de dados)**  
  
-   [DBCC SHRINKFILE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-shrinkfile-transact-sql)  
  
-   [Reduzir um arquivo](../databases/shrink-a-file.md)  
  
 **Para monitorar eventos de redução de arquivo de log**  
  
-   [Log File Auto Shrink Event Class](../event-classes/log-file-auto-shrink-event-class.md).  
  
 `To monitor log space`  
  
-   [DBCC SQLPERF &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-sqlperf-transact-sql)  
  
-   [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql) (Consulte as colunas **size**, **max_size** e **growth** do arquivo ou arquivos de log.)  
  
> [!NOTE]  
>  A redução de arquivos de log e do banco de dados pode ser configurada para ocorrer automaticamente. Contudo, não é recomendável a redução automática, e a propriedade de banco de dados `autoshrink` é definida como FALSE por padrão. Se `autoshrink` for configurada como TRUE, a redução automática reduzirá o tamanho de um arquivo apenas quando mais de 25 por cento de seu espaço estiver inutilizado. O arquivo é reduzido de forma que 25% de seu tamanho seja de espaço não utilizado ou ele tenha o tamanho original, o que for maior. Para obter informações sobre como alterar a configuração do `autoshrink` propriedade, consulte [exibir ou alterar as propriedades de um banco de dados](../databases/view-or-change-the-properties-of-a-database.md)-usar o **redução automática** propriedade o **opções**página- ou [opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)-use a opção AUTO_SHRINK.  
  
  
##  <a name="AddOrEnlarge"></a> Adicionar ou aumentar um arquivo de Log  
 Se desejar, você também pode obter mais espaço aumentando o arquivo de log existente (se houver espaço no disco) ou adicionando um arquivo de log ao banco de dados, geralmente em um disco diferente.  
  
-   Para adicionar um arquivo de log ao banco de dados, use a cláusula ADD LOG FILE da instrução ALTER DATABASE. Adicionar um arquivo de log permite o crescimento do log.  
  
-   Para aumentar o arquivo de log, use a cláusula MODIFY FILE da instrução ALTER DATABASE, especificando a sintaxe SIZE e MAXSIZE. Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
  
##  <a name="tempdbOptimize"></a> Otimizar o tamanho do Log de transações tempdb  
 Reinicializar uma instância de servidor redimensiona o log de transações do banco de dados **tempdb** ao seu tamanho original, antes do crescimento automático. Isso pode reduzir o desempenho do log de transações do **tempdb** . Você pode evitar essa sobrecarga aumentando o tamanho do log de transações do **tempdb** depois de iniciar ou reinicializar a instância de servidor. Para obter mais informações, confira [tempdb Database](../databases/tempdb-database.md).  
  
  
##  <a name="ControlGrowth"></a> Controlar o crescimento de um arquivo de Log de transações  
 Você pode usar a instrução [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql) para gerenciar o crescimento de um arquivo de log de transações. Observe o seguinte:  
  
-   Para alterar o tamanho do arquivo atual em unidades KB, MB, GB e TB, use a opção SIZE.  
  
-   Para alterar o incremento de crescimento, use a opção FILEGROWTH. Um valor 0 indica que o crescimento automático está definido como off e nenhum espaço adicional é permitido. Um pequeno crescimento automático em um arquivo de log também pode prejudicar o desempenho. O incremento de crescimento do arquivo em um arquivo de log deve ser suficientemente grande para evitar a expansão frequente. O incremento de crescimento padrão de 10 por cento, em geral, é satisfatório.  
  
     Para obter informações sobre como alterar a propriedade de crescimento do arquivo em um arquivo de log, consulte [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
-   Para controlar ao máximo o tamanho de um arquivo de log em unidades KB, MB, GB e TB, ou para definir o crescimento como UNLIMITED, use a opção MAXSIZE.  
  
  
## <a name="see-also"></a>Consulte também  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Solução de problemas de um log de transação completa &#40;Erro do SQL Server 9002&#41;](troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
  
