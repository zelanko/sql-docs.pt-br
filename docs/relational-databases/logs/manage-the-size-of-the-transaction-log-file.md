---
title: Gerenciar o tamanho do arquivo de log de transações | Microsoft Docs
ms.custom: ''
ms.date: 01/05/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], size management
- manage log size
- log size, manage
ms.assetid: 3a70e606-303f-47a8-96d4-2456a18d4297
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e4558680d089b0da1c756524e3cdab5d38c4ba74
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="manage-the-size-of-the-transaction-log-file"></a>Gerenciar o tamanho do arquivo de log de transações
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Este tópico aborda como monitorar o tamanho de um log de transações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], reduzir o log de transações, adicionar ou aumentar um arquivo de log de transações, otimizar a taxa de crescimento do log de transações de **tempdb** e controlar o crescimento de um arquivo de log de transações.  

##  <a name="MonitorSpaceUse"></a>Monitorar o uso do espaço de log  
Monitore o uso do espaço de log usando [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md). Essa DMV retorna informações sobre a quantidade de espaço de log usada atualmente e indica quando o log de transações precisa de truncamento. 

Para obter informações sobre o tamanho do arquivo de log atual, seu tamanho máximo e a opção de crescimento automático para o arquivo, você também pode usar as colunas **size**, **max_size** e **growth** para esse arquivo de log em [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md).  
  
> [!IMPORTANT]
> Evite sobrecarregar o disco de log. Verifique se o armazenamento de log pode suportar os requisitos de [IOPS](http://wikipedia.org/wiki/IOPS) e baixa latência da carga transacional. 
  
##  <a name="ShrinkSize"></a> Reduzir o tamanho do arquivo de log  
 Para reduzir o tamanho físico de um arquivo de log físico, você deve reduzir o arquivo de log. Isso será útil se você souber que um arquivo de log de transações contém espaço não utilizado. É possível reduzir um arquivo de log somente enquanto o banco de dados estiver online e se, pelo menos, um [VLF (arquivo de log virtual)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) estiver livre. Em alguns casos, talvez não seja possível reduzir o log antes do próximo truncamento de log.  
  
> [!NOTE]
> Fatores como uma transação de execução longa, que mantém [VLFs](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) ativos por um período extenso, podem restringir a redução de log ou até mesmo impedir que o log seja reduzido. Para obter informações, consulte [Fatores que podem atrasar o truncamento de log](../../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation).  
  
A redução de um arquivo de log remove um ou mais [VLFs](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) que não mantêm nenhuma parte do log lógico (ou seja, *VLFs inativos*). Quando um arquivo de log de transações é reduzido, os VLFs inativos são removidos do final do arquivo de log para reduzir o log para aproximadamente o tamanho do destino. 

> [!IMPORTANT]
> Antes de reduzir o log de transações, tenha em mente os [Fatores que podem atrasar o truncamento de log](../../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation). Se o espaço de armazenamento for necessário novamente após a redução de um log, o log de transações aumentará novamente e, fazendo isso, introduzirá uma sobrecarga de desempenho durante as operações de aumento do log. Para obter mais informações, consulte as [Recomendações](#Recommendations) neste tópico.
  
 **Reduzir um arquivo de log (sem reduzir os arquivos do banco de dados)**  
  
-   [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
  
-   [Reduzir um arquivo](../../relational-databases/databases/shrink-a-file.md)  
  
 **Monitorar eventos de redução de arquivo de log**  
  
-   [Log File Auto Shrink Event Class](../../relational-databases/event-classes/log-file-auto-shrink-event-class.md).  
  
 **Monitorar espaço de log**  
  
-   [sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)  
  
-   [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) (Consulte as colunas **size**, **max_size** e **growth** do arquivo ou arquivos de log.)  
  
##  <a name="AddOrEnlarge"></a> Adicionar ou aumentar um arquivo de log  
Também é possível obter mais espaço aumentando o arquivo de log existente (se houver espaço em disco) ou adicionando um arquivo de log ao banco de dados, geralmente em um disco diferente. Um arquivo de log de transações é suficiente, a menos que o espaço de log esteja se esgotando e o espaço em disco também esteja se esgotando no volume que contém o arquivo de log.   
  
-   Para adicionar um arquivo de log ao banco de dados, use a cláusula `ADD LOG FILE` da instrução `ALTER DATABASE`. Adicionar um arquivo de log permite o crescimento do log.  
-   Para aumentar o arquivo de log, use a cláusula `MODIFY FILE` da instrução `ALTER DATABASE`, especificando a sintaxe `SIZE` e `MAXSIZE`. Para obter mais informações, consulte [Opções de arquivo e grupo de arquivos de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).  

Para obter mais informações, consulte as [Recomendações](#Recommendations) neste tópico.
    
##  <a name="tempdbOptimize"></a> Otimizar o tamanho do log de transações tempdb  
 Reinicializar uma instância de servidor redimensiona o log de transações do banco de dados **tempdb** ao seu tamanho original, antes do crescimento automático. Isso pode reduzir o desempenho do log de transações do **tempdb** . 
 
 Você pode evitar essa sobrecarga aumentando o tamanho do log de transações do **tempdb** depois de iniciar ou reinicializar a instância de servidor. Para obter mais informações, confira [tempdb Database](../../relational-databases/databases/tempdb-database.md).  
  
##  <a name="ControlGrowth"></a> Controlar o crescimento de um arquivo de log de transações  
 Use a instrução [Opções de arquivo e grupo de arquivos de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) para gerenciar o aumento de um arquivo de log de transações. Observe o seguinte:  
  
-   Para alterar o tamanho atual do arquivo em unidades de KB, MB, GB e TB, use a opção `SIZE`.  
-   Para alterar o incremento de aumento, use a opção `FILEGROWTH`. Um valor 0 indica que o crescimento automático está definido como off e nenhum espaço adicional é permitido.  
-   Para controlar o tamanho máximo de um arquivo de log em unidades de KB, MB, GB e TB ou para definir o aumento como UNLIMITED, use a opção `MAXSIZE`.  

Para obter mais informações, consulte as [Recomendações](#Recommendations) neste tópico.

## <a name="Recommendations"></a> Recomendações
Estas são algumas recomendações gerais ao trabalhar com arquivos de log de transações:

-   O incremento de aumento automático do log de transações, conforme definido pela opção `FILEGROWTH`, deve ser grande o suficiente para se manter à frente das necessidades das transações da carga de trabalho. O incremento de crescimento do arquivo em um arquivo de log deve ser suficientemente grande para evitar a expansão frequente. Um ponteiro válido para dimensionar corretamente um log de transações é monitorar a quantidade de log ocupado durante:
    -  O tempo necessário para executar um backup completo, pois os backups de log não podem ocorrer até que ele seja concluído.
    -  O tempo necessário para as maiores operações de manutenção de índice.
    -  O tempo necessário para executar o maior lote em um banco de dados.

-   Ao definir **aumento automático** para arquivos de dados e de log usando a opção `FILEGROWTH`, talvez seja preferível defini-lo em **tamanho** em vez de em **percentual**, a fim de permitir um melhor controle da taxa de aumento, pois o percentual é um valor que aumenta constantemente.
    -  Tenha em mente de que os logs de transações não podem utilizar a [Inicialização Instantânea de Arquivo](../../relational-databases/databases/database-instant-file-initialization.md) e, portanto, tempos de aumento de log estendidos são especialmente críticos. 
    -  Como uma melhor prática, não defina o valor da opção `FILEGROWTH` como superior a 1.024 MB para logs de transações. Os valores padrão para a opção `FILEGROWTH` são:  
  
      |Versão|Valores padrão|  
      |-------------|--------------------|  
      |A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|Dados 64 MB. Arquivos de log 64 MB.|  
      |A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Dados 1 MB. Arquivos de log 10%.|  
      |Antes do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Dados 10%. Arquivos de log 10%.|  

-   Um pequeno incremento de aumento pode gerar um número excessivo de [VLFs](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) pequenos e pode reduzir o desempenho. Para determinar a distribuição ideal de VLF para o tamanho atual do log de transações de todos os bancos de dados em uma instância determinada e os incrementos de crescimento necessários para alcançar o tamanho necessário, consulte este [script](http://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs).

-   Um grande incremento de aumento pode gerar um número pequeno de [VLFs](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) grandes e também pode afetar o desempenho. Para determinar a distribuição ideal de VLF para o tamanho atual do log de transações de todos os bancos de dados em uma instância determinada e os incrementos de crescimento necessários para alcançar o tamanho necessário, consulte este [script](http://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs). 

-   Mesmo com o aumento automático habilitado, você pode receber uma mensagem informando que o log de transações está cheio, caso ele não possa aumentar rápido o suficiente para atender às necessidades da consulta. Para obter mais informações sobre como alterar o incremento de aumento, consulte [Opções de arquivo e grupo de arquivos de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)

-   Ter vários arquivos de log em um banco de dados não melhora o desempenho de forma alguma, porque os arquivos de log de transações não usam o [preenchimento proporcional](../../relational-databases/pages-and-extents-architecture-guide.md#ProportionalFill) como arquivos de dados no mesmo grupo de arquivos.  

-   Os arquivos de log podem ser definidos para serem reduzidos automaticamente. No entanto, isso **não é recomendável** e a propriedade de banco de dados **auto_shrink** é definida como FALSE por padrão. Se **auto_shrink** for definido como TRUE, a redução automática reduzirá o tamanho de um arquivo apenas quando mais de 25% de seu espaço estiver inutilizado. 
    -   O arquivo é reduzido de forma que 25% de seu tamanho seja de espaço não utilizado ou ele tenha o tamanho original, o que for maior. 
    -   Para obter informações sobre como alterar a configuração da propriedade **auto_shrink**, consulte [Exibir ou alterar as propriedades de um banco de dados](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md) e [Opções de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). 
  
## <a name="see-also"></a>Confira também  
[BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
[Solução de problemas de um log de transações cheio &#40;Erro 9002 do SQL Server &#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)    
[Guia de gerenciamento e arquitetura de backups de log de transações no log de transações do SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Backups)    
[Backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)    
[Opções de arquivo e grupo de arquivos de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)
