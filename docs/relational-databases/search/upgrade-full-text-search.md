---
title: Atualizar a pesquisa de texto completo | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], installing
- migrating full-text indexes [SQL Server]
- upgrading Full-Text Search
- installing Full-Text Search
- full-text search [SQL Server], upgrading
ms.assetid: 2fee4691-f2b5-472f-8ccc-fa625b654520
caps.latest.revision: "106"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e544e5cefe8b935086b93ac7f30acd033a8462aa
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="upgrade-full-text-search"></a>Atualizar pesquisa de texto completo
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] A atualização da pesquisa de texto completo para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] é feita durante a instalação e quando os arquivos de banco de dados e os catálogos de texto completo da versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são anexados, restaurados ou copiados por meio do Assistente para Copiar Banco de Dados.  
  
  
##  <a name="Upgrade_Server"></a> Atualizar uma instância do servidor  
 Em uma atualização no local, uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] é configurada lado a lado com a versão antiga do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e os dados são migrados. Se a pesquisa de texto completo estava instalada na versão antiga do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , uma versão nova da pesquisa de texto completo será instalada automaticamente. A instalação lado a lado significa que cada um dos componentes a seguir existe no nível de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Separadores de palavras, lematizadores e filtros  
 Agora cada instância usa seu próprio conjunto de separadores de palavras, lematizadores e filtros, em vez de utilizar a versão do sistema operacional desses componentes. Esses componentes também são mais fáceis de registrar e configurar por instância. Para obter mais informações, consulte [Configurar e gerenciar separadores de palavras e lematizadores de pesquisa](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md) e [Configurar e gerenciar filtros para pesquisa](../../relational-databases/search/configure-and-manage-filters-for-search.md).  
  
 Host do daemon de filtro  
 Os hosts do daemon de filtro de texto completo são processos que carregam e orientam com segurança os componentes externos extensíveis usados para índice e consulta, como separadores de palavras, lematizadores e filtros, sem comprometer a integridade do Mecanismo de Texto Completo. Uma instância de servidor usa um processo multi-threaded para todos os filtros multi-threaded e um processo single-threaded para todos os filtros single-threaded.  
  
> [!NOTE]  
>  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] introduziu uma conta de serviço para o serviço Iniciador FDHOST (MSSQLFDLauncher). Esse serviço propaga as informações da conta de serviço para os processos de host do daemon de filtro de uma dada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter informações sobre como configurar a conta de serviço, consulte [Definir a conta de serviço do Iniciador do Daemon de Filtro de Texto Completo](../../relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md).  
  
 No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], cada índice de texto completo reside em um catálogo de texto completo que pertence a um grupo de arquivos, tem um caminho físico e é tratado como um arquivo de banco de dados. No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versões posteriores, um catálogo de texto completo é um objeto lógico ou virtual que contém um grupo de índices de texto completo. Por isso, um novo catálogo de texto completo não é tratado como um arquivo de banco de dados com um caminho físico. No entanto, durante a atualização de qualquer catálogo de texto completo que contém arquivos de dados, é criado um novo grupo de arquivos no mesmo disco. Isso mantém o antigo comportamento de E/S do disco após a atualização. Qualquer índice de texto completo desse catálogo será colocado no novo grupo de arquivos se existir o caminho raiz. Se o caminho do antigo catálogo de texto completo for inválido, a atualização manterá o índice de texto completo no mesmo grupo de arquivos que a tabela base ou, no caso de uma tabela particionada, no grupo de arquivos primário.  
  
  
##  <a name="FT_Upgrade_Options"></a> Opções de atualização de texto completo  
 Na atualização de uma instância de servidor para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], a interface do usuário permite escolher uma das opções de atualização de texto completo a seguir.  
  
**Importar**  
 Os catálogos de texto completo são importados. A importação costuma ser consideravelmente mais rápida do que a recompilação. Por exemplo, quando é usada apenas uma CPU, a importação é executada cerca de 10 vezes mais rápido do que a recompilação. No entanto, um catálogo de texto completo importado não usará os novos separadores de palavras instalados com a versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para garantir a consistência nos resultados da consulta, os catálogos de texto completo precisam ser recompilados.  
  
> [!NOTE]  
>  A recompilação pode ser executada no modo multi-threaded e, se houver mais de 10 CPUs disponíveis, ela poderá ser executada mais rápido do que a importação se você permitir que a recompilação use todas as CPUs.  
  
 Se um catálogo de texto completo não estiver disponível, os índices de texto completo associados serão recompilados. Essa opção está disponível apenas para bancos de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
 Para obter informações sobre o impacto da importação do índice de texto completo, consulte "Considerações sobre como escolher uma opção de atualização de texto completo", mais adiante neste tópico.  
  
 **Recompilar**  
 Os catálogos de texto completo são recompilados usando-se os separadores de palavras novos e aprimorados. A recompilação de índices pode demorar um pouco, e uma quantidade significativa de memória e CPU pode ser necessária após a atualização.  
  
 **Redefinir**  
 Os catálogos de texto completo são redefinidos. Quando atualizados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], os arquivos de catálogo de texto completo são removidos, mas os metadados dos catálogos e dos índices de texto completo são preservados. Depois de serem atualizados, todos os índices de texto completo são desabilitados para o controle de alteração e os rastreamentos não são iniciados automaticamente. O catálogo permanecerá vazio até você executar uma população completa manualmente, depois que a atualização for concluída.  
  
##  <a name="Choosing_Upgade_Option"></a> Considerações sobre como escolher uma opção de atualização de texto completo  
 Ao escolher a opção de atualização para sua atualização, considere o seguinte:  
  
-   Você precisa de consistência nos resultados da consulta?  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instala novos separadores de palavras para uso pela Pesquisa semântica e de texto completo. Os separadores de palavras são usados na indexação e na consulta. Se você não recriar os catálogos de texto completo, seus resultados da pesquisa poderão ser inconsistentes. Se você emitir uma consulta de texto completo que procura uma frase que é interrompida diferentemente pelo separador de palavras em uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o separador de palavras atual, um documento ou linha contendo a frase talvez não seja recuperada. Isso ocorre porque as frases indexadas foram quebradas usando uma lógica diferente da usada pela consulta. A solução é preencher novamente (recompilar) os catálogos de texto completo com os novos separadores de palavras de forma que os comportamentos de tempo de indexação e de consulta sejam idênticos. Você pode escolher a opção Recriar para fazer isso ou executar a recompilação manualmente após escolher a opção Importar.  
  
-   Algum índice de texto completo foi compilado em colunas de chave de texto completo integer?  
  
     A recompilação faz otimizações internas que, em alguns casos, melhoram o desempenho de consultas do índice de texto completo atualizado. Especificamente, se você tiver catálogos de texto completo que contêm índices de texto completo para os quais a coluna de chave de texto completo da tabela base é do tipo de dados integer, a recompilação atingirá o desempenho ideal de consultas de texto completo depois da atualização. Nesse caso, é altamente recomendável usar a opção **Recriar** .  
  
    > [!NOTE]  
    >  Para os índices de texto completo do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], é recomendável que a coluna que funciona como a chave de texto completo seja um tipo de dados integer. Para obter mais informações, consulte [Melhorar o desempenho de índices de texto completo](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md).  
  
-   Qual é a prioridade para colocar a instância de servidor online?  
  
     A importação ou a recompilação durante a atualização usa muitos recursos da CPU, o que faz com que o restante da instância do servidor demore para ser atualizado e ficar online. Se colocar a instância do servidor online o mais rápido possível é importante para você e se você deseja executar uma população manual depois da atualização, a opção **Redefinir** é a mais adequada.  
  
## <a name="ensure-consistent-query-results-after-importing-a-full-text-index"></a>Assegurar resultados de consulta consistentes após importar um índice de texto completo  
 Se um catálogo de texto completo foi importado durante a atualização de um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], podem ocorrer incompatibilidades entre a consulta e o conteúdo do índice de texto completo devido a diferenças no comportamento dos antigos e dos novos separadores de palavras. Nesse caso, para garantir compatibilidade total entre as consultas e o conteúdo do índice de texto completo, escolha uma das opções a seguir:  
  
-   Recompilar o catálogo de texto completo que contém o índice de texto completo ([ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)*catalog_name* REBUILD)  
  
-   Emitir FULL POPULATION no índice de texto completo ([ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) ON *table_name* START FULL POPULATION).  
  
 Para obter mais informações sobre separadores de palavras, consulte [Configurar e gerenciar separadores de palavras e lematizadores para pesquisa](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
## <a name="upgrade-noise-word-files-to-stoplists"></a>Atualizar arquivos de palavra de ruído para listas de palavras irrelevantes (stoplist)  
Quando um banco de dados é atualizado do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], os arquivos de palavras de ruído não são mais usados. No entanto, os antigos arquivos de palavras de ruído ficam armazenados na pasta FTDATA\ FTNoiseThesaurusBak, e você poderá usá-los posteriormente quando atualizar ou criar as listas de palavras irrelevantes do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
 Depois de atualizar do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]:  
  
-   Se você nunca adicionou, modificou ou excluiu arquivos de palavras de ruído da sua instalação do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], a lista de palavras irrelevantes do sistema deve atender às suas necessidades.  
  
-   Se os arquivos da palavra de ruído foram modificados no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], essas modificações serão perdidas durante a atualização. Para recriar essas atualizações, recrie manualmente essas modificações na lista de palavras irrelevantes correspondente do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Para obter mais informações, consulte [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md).  
  
-   Caso você não deseje aplicar palavras irrelevantes aos índices de texto completo (por exemplo, se você excluiu ou apagou os arquivos de palavras de ruído da instalação do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]), desative a lista de palavras irrelevantes (stoplist) de cada índice de texto completo atualizado. Execute a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] (substituindo *database* pelo nome do banco de dados atualizado e *table* pelo nome da *tabela*):  
  
    ```  
    Use database;   
    ALTER FULLTEXT INDEX ON table  
       SET STOPLIST OFF;  
    GO  
    ```  
  
     A cláusula STOPLIST OFF remove a filtragem de palavras irrelevantes e disparará a população da tabela, sem filtrar nenhuma das palavras consideradas palavras de ruído.  
  
## <a name="backup-and-imported-full-text-catalogs"></a>Backup e catálogos de texto completo importados  
 Nos catálogos de texto completo que são recompilados ou redefinidos durante a atualização (e nos novos catálogos de texto completo), o catálogo de texto completo é um conceito lógico e não reside em um grupo de arquivos. Portanto, para fazer backup de um catálogo de texto completo no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], é necessário identificar cada grupo de arquivos que contém um índice de texto completo do catálogo e fazer backup de cada um deles. Para obter mais informações, consulte [Fazer backup e restaurar índices e catálogos de texto completo](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md).  
  
 Nos catálogos de texto completo importados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o catálogo de texto completo ainda é um arquivo de banco de dados em seu próprio grupo de arquivos. O processo de backup do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para catálogos de texto completo ainda é aplicável, a diferença é que o serviço MSFTESQL não existe no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter informações sobre o processo do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , consulte [Backing Up and Restoring Full-Text Catalogs](http://go.microsoft.com/fwlink/?LinkId=209154) (Backup e restauração de catálogos de texto completo) nos Manuais Online do SQL Server 2005.  
  
##  <a name="Upgrade_Db"></a> Migrando índices de texto completo ao atualizar um banco de dados para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 Os arquivos de banco de dados e catálogos de texto completo de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser atualizados para uma instância de servidor do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] por meio de anexação, restauração ou do Assistente para Copiar Banco de Dados. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] os índices de texto completo, se houver algum, serão importados, redefinidos ou recompilados. A propriedade de servidor **upgrade_option** controla qual opção de atualização de texto completo é usada pela instância de servidor durante essas atualizações de banco de dados.  
  
 Após anexar, restaurar ou copiar qualquer banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o banco de dados se torna imediatamente disponível e, em seguida, é atualizado de forma automática. Dependendo da quantidade de dados a serem indexados, a importação pode levar várias horas, e a recriação pode ser até dez vezes mais demorada. Lembre-se também de que, quando a opção de atualização estiver definida como Importar, se não houver um catálogo de texto completo disponível, os índices de texto completo associados serão recompilados.  
  
 **Para alterar o comportamento de atualização de texto completo em uma instância de servidor**  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]: Usar a ação da **opção\_de atualização** do [sp\_fulltext\_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **:** Use a **Opção de Atualização de Texto Completo** da caixa de diálogo **Propriedades do Servidor** . Para obter informações, consulte [Gerenciar e monitorar a pesquisa de texto completo em uma instância do servidor](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md).  
  
##  <a name="Considerations_for_Restore"></a> Considerações sobre a restauração de um Catálogo de texto completo do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 Um método de atualização dos dados de texto completo de um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] consiste em restaurar um backup completo do banco de dados para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Durante a importação de um catálogo de texto completo do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , é possível fazer backup e restaurar o banco de dados e o arquivo de catálogo. O comportamento é o mesmo no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
-   O backup completo do banco de dados incluirá o catálogo de texto completo. Para consultar o catálogo de texto completo, use o nome de arquivo do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , sysft_+*catalog-name*.  
  
-   Se o catálogo de texto completo estiver offline, ocorrerá falha no backup.  
  
 Para obter mais informações sobre como fazer o backup e a restauração de catálogos de texto completo do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , consulte [Fazer backup e restaurar índices e catálogos de texto completo](http://go.microsoft.com/fwlink/?LinkId=121052) e [Restauração por etapas e índices de texto completo](http://go.microsoft.com/fwlink/?LinkId=121053)nos Manuais Online do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
 Quando o banco de dados for restaurado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], um novo arquivo de banco de dados será criado para o catálogo de texto completo. O nome padrão desse arquivo é ftrow_*catalog-name*.ndf. Por exemplo, se o *catalog-name* for `cat1`, o nome padrão do arquivo de banco de dados do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] será `ftrow_cat1.ndf`. Porém, se o nome padrão já estiver sendo usado no diretório de destino, o novo arquivo de banco de dados será chamado `ftrow_`*catalog-name*`{`*GUID*`}.ndf`, em que *GUID* é o Identificador Global Exclusivo do novo arquivo.  
  
 Depois que os catálogos foram importados, o **sys.database_files** e **sys.master_file**s são atualizadas para remover as entradas do catálogo e a coluna **path** em **sys.fulltext_catalogs** é definida como NULL.  
  
 **Para fazer o backup de um banco de dados**  
  
-   [Backups de bancos de dados completos &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)  
  
-   [Backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md) (apenas no modelo de recuperação completa)  
  
 **Para restaurar um backup de banco de dados**  
  
-   [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
  
-   [Restaurações completas de banco de dados &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir usa a cláusula MOVE na instrução [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) para restaurar um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] denominado `ftdb1`. O banco de dados, o log e os arquivos de catálogo do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] são movidos para novos locais da instância de servidor do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , como segue:  
  
-   O arquivo de banco de dados, `ftdb1.mdf`, é movido para `C:\Program Files\Microsoft SQL Server\MSSQL.1MSSQL13.MSSQLSERVER\MSSQL\DATA\ftdb1.mdf`.  
  
-   O arquivo de log, `ftdb1_log.ldf`, é movido para um diretório de log da unidade do disco de log, *log_drive*`:\`*log_directory*`\ftdb1_log.ldf`.  
  
-   Os arquivos de catálogo que correspondem ao catálogo `sysft_cat90` são movidos para `C:\temp`. Depois de importados, os índices de texto completo são colocados automaticamente em um arquivo de banco de dados (C:\ftrow_sysft_cat90.ndf), e o diretório C:\temp é excluído.  
  
```  
RESTORE DATABASE [ftdb1] FROM  DISK = N'C:\temp\ftdb1.bak' WITH  FILE = 1,  
   MOVE N'ftdb1' TO N'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\ftdb1.mdf',  
    MOVE N'ftdb1_log' TO N'log_drive:\log_directory\ftdb1_log.ldf',  
    MOVE N'sysft_cat90' TO N'C:\temp';  
```  
  
##  <a name="Attaching_2005_ft_catalogs"></a> Anexando um banco de dados do SQL Server 2005 ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores, um catálogo de texto completo é um conceito lógico que se refere a um grupo de índices de texto completo. O catálogo de texto completo é um objeto virtual que não pertence a nenhum grupo de arquivos. No entanto, quando você anexa um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que contém arquivos de catálogo de texto completo a uma instância de servidor do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , os arquivos de catálogo são anexados de seus locais anteriores junto com os outros arquivos de banco de dados, assim como ocorre no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 O estado de cada catálogo de texto completo anexado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] é o mesmo de quando o banco de dados foi desanexado do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Se uma população de índice de texto completo for suspensa pela operação de desanexação, ela será retomada no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], e o índice de texto completo ficará disponível para pesquisa de texto completo.  
  
 Se o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não encontrar um arquivo de catálogo de texto completo ou se o arquivo de texto completo foi movido durante a operação de anexação sem que fosse especificado um novo local, o comportamento dependerá da opção de atualização de texto completo selecionada. Se a opção de atualização de texto completo for **Importar** ou **Recriar**, o catálogo de texto completo anexado será recriado. Se a opção de atualização de texto completo for **Redefinir**, o catálogo de texto completo anexado será redefinido.  
  
 Para obter mais informações sobre desanexar e anexar um banco de dados, consulte [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md), [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md), [sp_attach_db](../../relational-databases/system-stored-procedures/sp-attach-db-transact-sql.md) e [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar a pesquisa de texto completo](../../relational-databases/search/get-started-with-full-text-search.md)   
 [Configurar e gerenciar separadores de palavras e lematizadores de pesquisa](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [Configurar e gerenciar filtros para pesquisa](../../relational-databases/search/configure-and-manage-filters-for-search.md)  
  
  
