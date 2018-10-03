---
title: Banco de dados tempdb | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 81d2bf84e758ccfd8664408a760e77700a323e0e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48141056"
---
# <a name="tempdb-database"></a>Banco de dados tempdb
  O banco de dados do sistema **tempdb** é um recurso global disponível a todos os usuários conectados a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e é usado para manter o seguinte:  
  
-   Os objetos de usuário temporários criados explicitamente como: tabelas temporárias globais ou locais, procedimentos armazenados temporários, variáveis de tabela ou cursores.  
  
-   Objetos internos criados por [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], por exemplo, tabelas de trabalho para armazenar resultados intermediários para spool ou classificação.  
  
-   Versões de linha geradas por transações de modificação de dados em um banco de dados que usa a leitura de confirmados usando transações de isolação de controle de versão de linha ou isolação de instantâneo.  
  
-   As versões de linhas geradas por meio de transações de modificação de dados para recursos como: operações de índice on-line, vários conjuntos de resultados ativos (MARS) e gatilhos AFTER.  
  
 As operações em **tempdb** são registradas minimamente. Isso permite que transações sejam revertidas. **tempdb** é recriado cada vez que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado, de modo que o sistema sempre começa com uma cópia limpa do banco de dados. As tabelas temporárias e procedimentos armazenados são descartados automaticamente ou desconectados e nenhuma conexão fica ativa quando o sistema é desligado. Portanto, nunca há nada em **tempdb** a ser gravado de uma sessão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra. As operações de backup e restauração não são permitidas em **tempdb**.  
  
## <a name="physical-properties-of-tempdb"></a>Propriedades físicas de tempdb  
 A tabela a seguir lista os valores iniciais de configuração dos dados **tempdb** e dos arquivos de log. Os tamanhos desses arquivos podem variar um pouco em diferentes edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Arquivo|Nome lógico|Nome físico|Aumento do arquivo|  
|----------|------------------|-------------------|-----------------|  
|Dados primários|tempdev|tempdb.mdf|Aumento automático de 10 por cento até que o disco está cheio|  
|Log|templog|templog.ldf|Aumento automático de 10 por cento até um máximo de 2 terabytes.|  
  
 O tamanho de **tempdb** pode afetar o desempenho de um sistema. Por exemplo, se o **tempdb** tamanho é muito pequeno, o processamento do sistema poderia ser muito ocupado com o crescimento automático do banco de dados para dar suporte a suas necessidades de carga de trabalho toda vez que você inicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode evitar essa sobrecarga aumentando o tamanho de **tempdb**.  
  
## <a name="performance-improvements-in-tempdb"></a>Melhorias de desempenho em tempdb  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **tempdb** o desempenho é aprimorado dos seguintes modos:  
  
-   As tabelas temporárias e variáveis de tabela podem ser colocadas em cache. O armazenamento em cache permite que as operações de descarte e criação de objetos temporários sejam executadas rapidamente e reduz a contenção de alocação de página.  
  
-   O protocolo de travamento da página de alocação é aprimorado. Isso reduz o número de travas de UP (atualização) usadas.  
  
-   A sobrecarga de logging para **tempdb** é reduzida. Isso reduz o consumo de largura de banda de E/S do disco no arquivo de log **tempdb** .  
  
-   O algoritmo para alocar páginas combinadas em **tempdb** é aprimorado.  
  
### <a name="moving-the-tempdb-data-and-log-files"></a>Movendo os arquivos de log e dados de tempdb  
 Para mover os dados e arquivos de log de **tempdb** , veja [Mover bancos de dados do sistema](system-databases.md).  
  
### <a name="database-options"></a>Opções de banco de dados  
 A tabela a seguir lista o valor padrão de cada opção de banco de dados no banco de dados **tempdb** e se a opção pode ser modificada. Para exibir as configurações atuais dessas opções, use a exibição de catálogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) .  
  
|Opção de banco de dados|Valor padrão|Pode ser modificado|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|Sim|  
|ANSI_NULL_DEFAULT|OFF|Sim|  
|ANSI_NULLS|OFF|Sim|  
|ANSI_PADDING|OFF|Sim|  
|ANSI_WARNINGS|OFF|Sim|  
|ARITHABORT|OFF|Sim|  
|AUTO_CLOSE|OFF|não|  
|AUTO_CREATE_STATISTICS|ON|Sim|  
|AUTO_SHRINK|OFF|não|  
|AUTO_UPDATE_STATISTICS|ON|Sim|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Sim|  
|CHANGE_TRACKING|OFF|não|  
|CONCAT_NULL_YIELDS_NULL|OFF|Sim|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Sim|  
|CURSOR_DEFAULT|GLOBAL|Sim|  
|Opções de disponibilidade de banco de dados|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|não<br /><br /> não<br /><br /> não|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Sim|  
|DB_CHAINING|ON|não|  
|ENCRYPTION|OFF|não|  
|NUMERIC_ROUNDABORT|OFF|Sim|  
|PAGE_VERIFY|CHECKSUM para novas instalações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> NONE para atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Sim|  
|PARAMETERIZATION|SIMPLE|Sim|  
|QUOTED_IDENTIFIER|OFF|Sim|  
|READ_COMMITTED_SNAPSHOT|OFF|não|  
|RECOVERY|SIMPLE|não|  
|RECURSIVE_TRIGGERS|OFF|Sim|  
|Opções do Service Broker|ENABLE_BROKER|Sim|  
|TRUSTWORTHY|OFF|não|  
  
 Para obter uma descrição dessas opções de banco de dados, veja [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
## <a name="restrictions"></a>Restrictions  
 As seguintes operações não podem ser executadas no banco de dados **tempdb** :  
  
-   Adição de grupos de arquivos  
  
-   Backup ou restauração de banco de dados.  
  
-   Alteração de agrupamento. O agrupamento padrão é o agrupamento de servidor.  
  
-   Alteração do proprietário do banco de dados. **tempdb** pertence a **sa**.  
  
-   Criação de um instantâneo do banco de dados  
  
-   Descartando o banco de dados.  
  
-   Descartando o usuário **convidado** do banco de dados.  
  
-   Habilitação do Change Data Capture.  
  
-   Participação no espelhamento de banco de dados.  
  
-   Remoção do grupo de arquivos primário, arquivo de dados primário ou arquivo de log.  
  
-   Renomeação do banco de dados ou grupo de arquivos primário.  
  
-   Execução de DBCC CHECKALLOC.  
  
-   Execução de DBCC CHECKCATALOG.  
  
-   Definindo o banco de dados como OFFLINE.  
  
-   Definindo o banco de dados ou grupo de arquivos primário como READ_ONLY.  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode criar objetos temporários no tempdb. Os usuários podem acessar somente seus próprios objetos, a menos que recebam permissões adicionais. É possível revogar a permissão de conexão ao tempdb para impedir um usuário de usar tempdb, mas isto não é recomendado porque algumas operações rotineiras exigem o uso de tempdb.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Opção SORT_IN_TEMPDB para índices](../indexes/indexes.md)  
  
 [Bancos de dados do sistema](system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [Mover arquivos de banco de dados](move-database-files.md)  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com tempdb no SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81216)  
  
  
