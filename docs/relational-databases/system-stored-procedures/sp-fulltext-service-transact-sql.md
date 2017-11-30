---
title: sp_fulltext_service (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_fulltext_service
- sp_fulltext_service_TSQL
dev_langs: TSQL
helpviewer_keywords:
- full-text search [SQL Server], properties
- sp_fulltext_service
- Full-Text Search Upgrade Option
ms.assetid: 17a91433-f9b6-4a40-88c4-8c704ec2de9f
caps.latest.revision: "79"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ac28028d1e888724417d1a313e229beb479e8ea2
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="spfulltextservice-transact-sql"></a>sp_fulltext_service (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades do servidor da pesquisa de texto completo para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_fulltext_service [ [@action=] 'action'   
     [ , [ @value= ] value ] ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@action=**] **'***ação***'**  
 É a propriedade a ser alterada ou redefinida. *ação* é **nvarchar (100),** sem nenhum padrão. Para obter uma lista de um*c*ção propriedades, suas descrições e os valores que podem ser definidos, consulte a tabela sob o *valor* argumento. Esse argumento retorna as seguintes propriedades: tipo de dados, valor em execução atual, valor mínimo ou máximo e status da reprovação, se aplicável.  
  
 [  **@value=**] *valor*  
 É o valor da propriedade especificada. *valor* é **sql_variant**, com um valor padrão de NULL. Se @value for nulo, **sp_fulltext_service** retorna a configuração atual. Essa tabela lista propriedades de ação, suas descrições e os valores que podem ser definidos.  
  
> [!NOTE]  
>  As ações a seguir serão removidas em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **clean_up**, **connect_timeout**, **data_timeout**, e **resource_ uso**. Evite usar essas ações em novos trabalhos de desenvolvimento e planeje a modificação dos aplicativos que as usam atualmente.  
  
|Ação|Tipo de dados|Description|  
|------------|---------------|-----------------|  
|**clean_up**|**int**|Com suporte somente para compatibilidade com versões anteriores. O valor padrão é sempre 0.|  
|**connect_timeout**|**int**|Com suporte somente para compatibilidade com versões anteriores. O valor padrão é sempre 0.|  
|**data_timeout**|**int**|Com suporte somente para compatibilidade com versões anteriores. O valor padrão é sempre 0.|  
|**load_os_resources**|**int**|Indica se os separadores de palavras, lematizadores e filtros do sistema operacional são registrados e usados com essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um dos seguintes:<br /><br /> 0 = Usa somente filtros e separadores de palavra específicos para essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = Carregar filtros e separadores de palavras do sistema operacional.<br /><br /> Por padrão, essa propriedade é desabilitada para impedir alterações de comportamento acidental em atualizações feitas no sistema operacional. A habilitação do uso de recursos do sistema operacional fornece acesso a recursos para idiomas e tipos de documento registrados no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Indexing Service que não têm um recurso específico de instância instalado. Se você habilitar o carregamento de recursos do sistema operacional, certifique-se de que os recursos do sistema operacional são binários assinados confiáveis; Caso contrário, eles não podem ser carregados quando **verify_signature** (veja abaixo) é definida como 1.|  
|**master_merge_dop**|**int**|Especifica o número de threads a ser usado pelo processo de mesclagem mestre. Esse valor não deve exceder o número de CPUs disponíveis ou núcleos de CPU.<br /><br /> Quando este argumento não é especificado, o serviço usa o menor de 4, ou o número de CPUs disponíveis ou núcleos de CPU.|  
|**pause_indexing**|**int**|Especifica se a indexação de texto completo deve ser pausada, se estiver em execução no momento, ou retomada, se estiver pausada no momento.<br /><br /> 0 = Retoma as atividades de indexação de texto completo para a instância do servidor.<br /><br /> 1 = Pausa as atividades de indexação de texto completo para a instância do servidor.|  
|**resource_usage**|**int**|Não tem nenhuma função no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versões posteriores e é ignorado.|  
|**update_languages**|NULL|Atualiza a lista de idiomas e filtros que estão registrados com pesquisa de texto completo. Os idiomas são especificados ao configurar indexação e em consultas de texto completo. Filtros são usados pelo host do daemon de filtro para extrair informações textuais de formatos de arquivo correspondentes, como. docx armazenado em tipos de dados, como **varbinary**, **varbinary (max)**, **imagem** , ou **xml**, para indexação de texto completo.<br /><br /> Para obter mais informações, consulte [View or Change Registered Filters and Word Breakers](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).|  
|**upgrade_option**|**int**|Controla como são migrados índices de texto completo ao atualizar um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para uma versão posterior. Essa propriedade se aplica à atualização anexando um banco de dados, restaurando um backup do banco de dados, restaurando um backup de arquivo ou copiando o banco de dados usando o Assistente para Copiar Banco de Dados.<br /><br /> Um dos seguintes:<br /><br /> 0 = os catálogos de texto completo são recompilados usando-se os separadores de palavras novos e aprimorados. A recompilação de índices pode demorar um pouco, e uma quantidade significativa de memória e CPU pode ser necessária após a atualização.<br /><br /> 1 = Os catálogos de texto completo são redefinidos. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] os arquivos de catálogos de texto completo são removidos, mas os metadados dos catálogos e dos índices de texto completo são preservados. Depois de serem atualizados, todos os índices de texto completo são desabilitados para o controle de alteração e os rastreamentos não são iniciados automaticamente. O catálogo permanecerá vazio até você executar uma população completa manualmente, depois que a atualização for concluída.<br /><br /> 2 = os catálogos de texto completo são importados. A importação costuma ser consideravelmente mais rápida do que a recompilação. Por exemplo, quando é usada apenas uma CPU, a importação é executada cerca de 10 vezes mais rápido do que a recompilação. Contudo, um catálogo de texto completo importado não usa os separadores de palavras novos e aprimorados, por isso pode ser necessário recompilar o catálogo de texto completo no futuro.<br /><br /> Observação: Recompilação pode ser executada no modo multi-threaded e, se houver mais de 10 CPUs disponíveis, ela poderá ser executada mais rapidamente do que a importação se você permitir que a recompilação use todas as CPUs.<br /><br /> Se um catálogo de texto completo não estiver disponível, os índices de texto completo associados serão recompilados. Essa opção está disponível apenas para bancos de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .<br /><br /> Para obter informações sobre como escolher uma opção de atualização de texto completo, consulte[Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md).<br /><br /> Observação: Para definir essa propriedade na [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], use o **Full-Text Upgrade Option** propriedade. Para obter informações, consulte [Gerenciar e monitorar a pesquisa de texto completo em uma instância do servidor](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md).|  
|**verify_signature**|**int**|Indica se apenas binários assinados são carregados pelo Mecanismo de Texto Completo. Por padrão, somente binários assinados confiáveis são carregados.<br /><br /> 1 = Verifica se somente binários assinados confiáveis são carregados (padrão).<br /><br /> 0 = Não verifica se binários são assinados.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **serveradmin** função fixa de servidor ou o administrador do sistema pode executar **sp_fulltext_service**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-updating-the-list-of-registered-languages"></a>A. Atualizando a lista de idiomas registrados  
 O exemplo a seguir atualiza a lista de idiomas registrados na pesquisa de texto completo.  
  
```  
EXEC sp_fulltext_service 'update_languages';  
GO  
```  
  
### <a name="b-changing-the-full-text-upgrade-option-to-reset-full-text-catalogs"></a>B. Alterando a opção de atualização de texto completo para redefinir catálogos de texto completo  
 O exemplo a seguir altera a opção de atualização de texto completo para redefinir catálogos de texto completo. Isso os remove completamente. Esse exemplo especifica a `@action` opcional e as palavras-chave `@value`.  
  
```  
EXEC sp_fulltext_service @action='upgrade_option', @value=1;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Pesquisa de Texto Completo](../../relational-databases/search/full-text-search.md)   
 [FULLTEXTSERVICEPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
