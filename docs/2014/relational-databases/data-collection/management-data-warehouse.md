---
title: Data warehouse de gerenciamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collector [SQL Server], management data warehouse
- data warehouse
- management data warehouse
ms.assetid: 9874a8b2-7ccd-494a-944c-ad33b30b5499
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 26af58e208527d155b5ddf3506be4509627c1f7e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52778448"
---
# <a name="management-data-warehouse"></a>data warehouse de gerenciamento
  O data warehouse de gerenciamento é um banco de dados relacional que contém os dados coletados de um servidor representa o destino da coleta de dados. Esses dados são usados para gerar os relatórios dos conjuntos de coleta de Dados do Sistema e também podem ser usados para criar relatórios personalizados.  
  
 A infraestrutura do coletor de dados define os trabalhos e os planos de manutenção necessários para implementar as políticas de retenção definidas pelo administrador do banco de dados.  
  
> [!IMPORTANT]  
>  Para esta versão do coletor de dados, o data warehouse de gerenciamento é criado com o modelo de recuperação simples para minimizar o registro. Você deve implementar o modelo de recuperação adequado para sua organização.  
  
## <a name="deploying-and-using-the-data-warehouse"></a>Implantando e usando o data warehouse  
 Você pode instalar o data warehouse de gerenciamento na mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que executa o coletor de dados. No entanto, se o desempenho ou os recursos do servidor forem um problema no servidor que está sendo monitorado, você poderá instalar o data warehouse de gerenciamento em outro computador.  
  
 Os esquemas necessários e seus objetos para os conjuntos de coleta do sistema predefinidos são criados quando você gera o data warehouse de gerenciamento. Os esquemas que são criados são principal e instantâneos. Um terceiro esquema, custom_snapshots, é criado quando os conjuntos de coleta definidos pelo usuário são criados, o que inclui itens de coleta que usam o tipo de coletor de Consultas T-SQL Genérico.  
  
###### <a name="core-schema"></a>Esquema principal  
 O esquema principal descreve as tabelas, os procedimentos armazenados e as exibições usados para organizar e identificar os dados coletados. Essas tabelas são compartilhadas entre todas as tabelas de dados criadas para tipos de coletores individuais. Esse esquema está bloqueado e só pode ser modificado pelo proprietário do banco de dados do data warehouse de gerenciamento. Os nomes das tabelas nesse esquema são prefixados por "core".  
  
 A tabela a seguir descreve as tabelas de banco de dados no esquema principal. Essas tabelas de banco de dados permitem que o coletor de dados rastreie o local de origem dos dados, quem os inseriu e quando foram carregados no data warehouse.  
  
|Nome da tabela|Descrição|  
|----------------|-----------------|  
|core.performance_counter_report_group_items|Armazena informações sobre como os relatórios do data warehouse de gerenciamento devem agrupar e agregar contadores de desempenho.|  
|core.snapshots_internal|Identifica cada novo instantâneo. Uma nova linha é inserida nessa tabela sempre que um pacote de carregamento inicia o carregamento de um novo lote de dados.|  
|core.snapshot_timetable_internal|Armazena informações sobre as horas do instantâneo. A hora do instantâneo é armazenada em uma tabela separada porque muitos instantâneos podem ocorrer praticamente ao mesmo tempo.|  
|core.source.info_internal|Esta tabela armazena informações sobre a fonte de dados. Esta tabela é atualizada sempre que um novo conjunto de coleta inicia o carregamento de dados no data warehouse.|  
|core.supported_collector_types_internal|Contém as IDs dos tipos de coletor registrados que podem carregar dados no data warehouse de gerenciamento. Essa tabela só é atualizada quando o esquema do warehouse é atualizado para suportar um novo tipo de coletor. Quando o data warehouse de gerenciamento é criado, essa tabela é populada com as IDs dos tipos de coletor fornecidos pelo coletor de dados.|  
|core.wait_categories|Contém as categorias usadas para agrupar tipos de espera de acordo com a característica wait_type.|  
|core.wait_types|Contém os tipos de espera reconhecidos pelo coletor de dados.|  
|core.purge_info_internal|Indica que foi feita uma solicitação para parar a remoção de dados do data warehouse de gerenciamento.|  
  
 As tabelas precedentes são usadas com tabelas de tipos de coletor para armazenar informações. Por exemplo, o tipo de coletor de Rastreamento do SQL Genérico usa as tabelas a seguir para armazenar dados de rastreamento:  
  
-   core.source_info_internal  
  
-   core.snapshots_internal  
  
-   snapshots.trace_info  
  
-   snapshots.trace_data  
  
###### <a name="snapshots-schema"></a>Esquema de instantâneos  
 O esquema de instantâneos descreve os objetos que precisam armazenar e atualizar dados coletados pelos tipos de coletores fornecidos. As tabelas neste esquema são fixas e não precisam ser alteradas durante o tempo de vida do tipo de coletor. Se houver necessidade de alterações, o esquema só poderá ser alterado por membros com função mdw_admin. Essas tabelas são criadas para armazenar os dados coletados pelos conjuntos de coleta de dados do sistema.  
  
 As tabelas a seguir ilustram uma parte do esquema do data warehouse de gerenciamento necessária para os conjuntos de coleta de atividades do servidor e estatísticas de consulta.  
  
-   Tabelas de recurso de nível de sistema  
  
    -   **snapshots.os_wait_stats**  
  
    -   **snapshots.os_latch_stats**  
  
    -   **snapshots.os_schedulers**  
  
    -   `snapshots.os_memory_clerks`  
  
    -   **snapshots.os_memory_nodes**  
  
    -   snapshots.sql_process_and_system_memory  
  
-   Atividade do sistema  
  
    -   snapshots.active_sessions_and_requests  
  
-   Estatísticas de consulta  
  
    -   snapshots.query_stats  
  
-   Estatísticas de E/S  
  
    -   `snapshots.io_virtual_file_stats`  
  
-   Texto e plano de consulta  
  
    -   snapshots.notable_query_text  
  
    -   snapshots.notable_query_plan  
  
-   Estatísticas de consultas normalizadas  
  
    -   snapshots.distinct_queries  
  
    -   snapshots.distinct_query_to_handle  
  
 **Esquema custom_snapshots**  
  
 Um esquema custom_snapshots descreve novas tabelas e exibições criadas quando os tipos de coletor padrão ou de terceiros são usados para criar conjuntos de coleta definidos pelo usuário. Qualquer tipo de coletor que exija uma nova tabela de dados para um item de coleta pode criar essa tabela neste esquema. Novas tabelas podem ser adicionadas a esse esquema por membros da função mdw_writer. Todas as outras alterações no esquema só poderão ser feitas por membros da função mdw_admin.  
  
 Você pode obter informações detalhadas sobre o tipo de dados e o conteúdo de colunas de tabelas do banco de dados lendo a documentação do procedimento armazenado do coletor de dados adequado para cada uma das tabelas.  
  
### <a name="best-practices"></a>Práticas recomendadas  
 Ao trabalhar com o data warehouse de gerenciamento, recomendamos que você siga estas práticas recomendadas:  
  
-   Não modifique o metadados de tabelas de data warehouse de gerenciamento a menos que você esteja adicionando um tipo de coletor novo.  
  
-   Não modifique os dados diretamente no data warehouse de gerenciamento. Alterar os dados que coletados invalida a legitimidade dos dados coletados.  
  
-   Em vez de usar as tabelas diretamente, use os procedimentos armazenados documentados e as funções fornecidas pelo coletor de dados para acessar instância e dados de aplicativo. Os nomes e as definições de tabelas podem ser alterados. Elas são alteradas quando você atualiza o aplicativo e talvez sejam alteradas em futuras versões.  
  
## <a name="change-history"></a>Histórico de alterações  
  
|Conteúdo atualizado|  
|---------------------|  
|Adicionada a tabela core.performance_counter_report_group_items à seção "Esquema principal".|  
|Atualizada a lista de tabelas na seção "Esquema de instantâneos". Adicionados snapshots.os_memory_clerks,snapshots.sql_process_and_system_memory e snapshots.io_virtual_file_stats. snapshots.os_process_memory e snapshots.distinct_query_stats foram removidos.|  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do data warehouse de gerenciamento &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/management-data-warehouse-stored-procedures-transact-sql)   
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql)   
 [Coleta de dados](data-collection.md)   
 [Exibir um relatório de conjuntos de coleta &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md)  
  
  
