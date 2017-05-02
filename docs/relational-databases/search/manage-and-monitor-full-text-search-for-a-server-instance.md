---
title: "Gerenciar e monitorar a pesquisa de texto completo em uma instância do servidor | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], about
- full-text search [SQL Server], server management
ms.assetid: 2733ed78-6d33-4bf9-94da-60c3141b87c8
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 657d78f548e8368ad2ff4c554fc6f731d7fb27fa
ms.lasthandoff: 04/11/2017

---
# <a name="manage-and-monitor-full-text-search-for-a-server-instance"></a>Gerenciar e monitorar a pesquisa de texto completo em uma instância do servidor
  A administração de texto completo para uma instância de servidor inclui:  
  
-   Tarefas de gerenciamento do sistema, como gerenciar o serviço Iniciador FDHOST (MSSQLFDLauncher), reiniciar o processo do daemon de filtro caso você altere as credenciais da conta de serviço, configurar as propriedades de texto completo no servidor e fazer backup de catálogos de texto completo. No nível do servidor, por exemplo, é possível especificar um idioma de texto completo padrão diferente do idioma padrão da instância do servidor como um todo.  
  
-   Configurar componentes linguísticos de texto completo (separadores de palavras e lematizadores, arquivo de dicionário de sinônimos e palavras irrelevantes e listas de palavras irrelevantes).  
  
-   Configurar um banco de dados de usuário para pesquisa de texto completo. Isto envolve criar um ou mais catálogos de texto completo para o banco de dados e definir um índice de texto completo em cada tabela ou exibição indexada em que você deseja executar consultas de texto completo.  
  
##  <a name="props"></a> Exibindo ou alterando as propriedades do servidor referentes à pesquisa de texto completo  
 Você pode exibir as propriedades de texto completo de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-view-and-change-server-properties-for-full-text-search"></a>Para exibir e alterar as propriedades do servidor de alterações para pesquisa de texto completo  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Propriedades do Servidor** , clique na página **Avançado** para exibir as informações do servidor sobre a pesquisa de texto completo. As propriedades de texto completo são:  
  
    -   **Idioma de Texto Completo Padrão**  
  
         Especifica um idioma padrão para colunas indexadas de texto completo. A análise linguística dos dados indexados de texto completo depende do idioma dos dados. O valor padrão dessa opção é o idioma do servidor. Para obter a linguagem que corresponde à configuração exibida, veja [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
  
    -   **Opção de Atualização de Texto Completo**  
  
         Essa propriedade do servidor controla a maneira como os índices de texto completo são migrados ao atualizar um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para uma versão posterior. Essa propriedade se aplica à atualização anexando um banco de dados, restaurando um backup do banco de dados, restaurando um backup de arquivo ou copiando o banco de dados usando o Assistente para Copiar Banco de Dados.  
  
         As alternativas são como segue:  
  
         **Importar**  
         Os catálogos de texto completo são importados. A importação costuma ser consideravelmente mais rápida do que a recompilação. Por exemplo, quando é usada apenas uma CPU, a importação é executada cerca de 10 vezes mais rápido do que a recompilação. Contudo, um catálogo de texto completo importado não usa os separadores de palavras novos e aprimorados introduzidos no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], por isso pode ser necessário recompilar o catálogo de texto completo no futuro.  
  
        > [!NOTE]  
        >  A recompilação pode ser executada no modo multi-threaded e, se houver mais de 10 CPUs disponíveis, ela poderá ser executada mais rápido do que a importação se você permitir que a recompilação use todas as CPUs.  
  
         Se um catálogo de texto completo não estiver disponível, os índices de texto completo associados serão recompilados. Essa opção está disponível apenas para bancos de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
         **Recriar**  
         Os catálogos de texto completo são recompilados usando-se os separadores de palavras novos e aprimorados. A recompilação de índices pode demorar um pouco, e uma quantidade significativa de memória e CPU pode ser necessária após a atualização.  
  
         **Redefinir**  
         Os catálogos de texto completo são redefinidos. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] os arquivos de catálogos de texto completo são removidos, mas os metadados dos catálogos e dos índices de texto completo são preservados. Depois de serem atualizados, todos os índices de texto completo são desabilitados para o controle de alteração e os rastreamentos não são iniciados automaticamente. O catálogo permanecerá vazio até você executar uma população completa manualmente, depois que a atualização for concluída.  
  
         Para obter informações sobre como escolher uma opção de atualização de texto completo, consulte[Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  
        > [!NOTE]  
        >  A opção de atualização de texto completo também pode ser definida com o uso da ação [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)**upgrade_option** .  
  
##  <a name="metadata"></a> Exibindo propriedades de servidor de texto completo adicionais  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] as funções podem ser utilizadas para obter o valor de diversas propriedades da pesquisa de texto completo no nível do servidor. Essas informações são úteis para administrar e solucionar problemas de pesquisa de texto completo.  
  
 A tabela a seguir lista propriedades de texto completo de uma instância de servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e suas funções [!INCLUDE[tsql](../../includes/tsql-md.md)] relacionadas.  
  
|Propriedade|Descrição|Função|  
|--------------|-----------------|--------------|  
|**IsFullTextInstalled**|Se o componente de texto completo está instalado com a instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[FULLTEXTSERVICEPROPERTY](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)<br /><br /> [SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md)|  
||||  
|**LoadOSResources**|Se os separadores de palavras e os filtros do sistema operacional estão registrados e são usados com essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|FULLTEXTSERVICEPROPERTY|  
|**VerifySignature**|Especifica se apenas binários assinados são carregados pelo Mecanismo de Texto Completo.|FULLTEXTSERVICEPROPERTY|  
  
##  <a name="monitor"></a> Monitorando a atividade de pesquisa de texto completo  
 Existem diversas exibições e funções de gerenciamento dinâmico que são úteis para monitorar a atividade de pesquisa de texto completo em uma instância do servidor.  
  
 **Para exibir informações sobre os catálogos de texto completo com atividade de população em andamento**  
  
-   [sys.dm_fts_active_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql.md)  
  
 **Para exibir a atividade atual de um processo de host do daemon de filtro**  
  
-   [sys.dm_fts_fdhosts &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-fdhosts-transact-sql.md)  
  
 **Para exibir informações sobre populações de índice em andamento**  
  
-   [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
 **Para exibir buffers de memória de um pool de memórias que são usados como parte de um rastreamento ou de um intervalo de rastreamento.**  
  
-   [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)  
  
 **Para exibir os pools de memórias compartilhadas disponíveis para o componente gatherer de texto completo em um rastreamento de texto completo ou em um intervalo de rastreamento de texto completo**  
  
-   [sys.dm_fts_memory_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)  
  
 **Para exibir informações sobre cada lote de indexação de texto completo**  
  
-   [sys.dm_fts_outstanding_batches &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md)  
  
 **Para exibir informações sobre os intervalos específicos relacionados a uma população em andamento**  
  
-   [sys.dm_fts_population_ranges &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-population-ranges-transact-sql.md)  
  
  
