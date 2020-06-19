---
title: Alterações recentes na pesquisa de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], breaking changes
- full-text catalogs [SQL Server], breaking changes
- breaking changes [full-text search]
- full-text indexes [SQL Server], breaking changes
ms.assetid: c55a6748-e5d9-4fdb-9a1f-714475a419c5
author: rothja
ms.author: jroth
ms.openlocfilehash: 260b1a303685ad9247154504400ef1519ecaa219
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936107"
---
# <a name="breaking-changes-to-full-text-search"></a>Alterações recentes na pesquisa de texto completo
  Este tópico descreve as alterações recentes feitas na pesquisa de texto completo. Essas alterações podem danificar aplicativos, scripts ou funcionalidades baseados em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Talvez você tenha esses problemas ao atualizar. Para obter mais informações, consulte [Use Upgrade Advisor to Prepare for Upgrades](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
## <a name="breaking-changes-in-full-text-search-in-sssql14"></a>Alterações mais recentes na pesquisa de texto completo no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Informações que virão posteriormente.  
  
## <a name="breaking-changes-in-full-text-search-in-sssql11"></a>Alterações mais recentes na pesquisa de texto completo no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="collation-changed-for-name-column-in-sysfulltext_languages"></a>Ordenação alterada para o nome Coluna em sys.fulltext_languages  
 A ordenação da coluna **name** do idioma na exibição do catálogo [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql) foi alterada da ordenação fixa do banco de dados Resource para a ordenação padrão selecionada para a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Esta alteração possibilitará comparar os valores na coluna **name** quando você unir a exibição [sys.syslanguages &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-syslanguages-transact-sql) com **sys.fulltext_languages**. Por exemplo, você pode consultar todos os bancos de dados onde o idioma de texto completo padrão é diferente do idioma de banco de dados padrão.  
  
## <a name="breaking-changes-in-full-text-search-in-sql-server-2008"></a>Analisando as alterações feitas na pesquisa de texto completo no SQL Server 2008  
 As últimas alterações a seguir aplicam-se à Pesquisar de texto completo entre o [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] e o [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e versões posteriores.  
  
|Recurso|Cenário|SQL Server 2005|SQL Server 2008 e versões posteriores|  
|-------------|--------------|---------------------|----------------------------------------|  
|[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) com tipos definidos pelo usuário (UDTs)|A chave de texto completo é um tipo definido pelo usuário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], por exemplo, `MyType = char(1)`.|A chave retornada é do tipo atribuído ao tipo definido pelo usuário.<br /><br /> No exemplo, isso seria **Char (1)**.|A chave retornada é do tipo definido pelo usuário. No exemplo, isso seria **com MyType**.|  
|parâmetro *top_n_by_rank* (das instruções CONTAINSTABLE e [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) [!INCLUDE[tsql](../includes/tsql-md.md)] )|*top_n_by_rank* consultas usando 0 como o parâmetro.|Falha com uma mensagem de erro, indicando que você deve usar um valor maior que zero.|Tem êxito, não retornando nenhuma linha.|  
|CONTAINSTABLE e **ItemCount**|Excluir linhas da tabela base antes do envio por push de alterações para MSSearch.|CONTAINSTABLE retorna registro fantasma. **ItemCount** não é alterado.|CONTAINSTABLE não retorna nenhum registro fantasma.|  
|**ItemCount**|A tabela contém colunas de tipo ou documentos nulos.|Além dos documentos indexados, os documentos que são nulos ou que têm tipos nulos são contados no valor **ItemCount** .|Somente documentos indexados são contados no valor **ItemCount** .|  
|Catálogo de **ItemCount**|Coluna blob com uma extensão NULL.|Ele é contado em **ItemCount** do catálogo|Ele não é contado em **ItemCount** do catálogo.|  
|**UniqueKeyCount**|Consultar uma contagem de chave exclusiva a partir de um catálogo, por exemplo, duas tabelas (table1 e table2) em que cada uma tem três palavras: word1, word2 e word3.|**UniqueKeyCount** = 9. A tabela a seguir resume como esse valor é obtido:<br /><br /> table1 = 3<br /><br /> EOF para índice de texto completo de table1 = 1<br /><br /> table2 = 3<br /><br /> EOF para índice de texto completo de table2 = 1<br /><br /> catálogo de texto completo = 1|Para cada tabela, **UniqueKeyCount** é o número de palavras-chave distintas + 1 (0xFF).  Isso não trata as mesmas palavras no > 1 doc como uma nova chave exclusiva.<br /><br /> Para um catálogo, **UniqueKeyCount** é a soma de **UniqueKeyCount** de cada uma das tabelas no catálogo. Palavras idênticas de tabelas diferentes são tratadas como chaves exclusivas. Nesse caso, a contagem de chaves exclusivas é 8.|  
|opção de nível de servidor **pré-calcular Rank**|Otimização do desempenho de consultas FREETEXTTABLE.|Quando a opção é definida como 1, as consultas FREETEXTtable especificadas com *top_n_by_rank* usam dados de classificação computados armazenados nos catálogos de texto completo.|Não tem suporte.|  
|[sp_fulltext_pendingchanges](/sql/relational-databases/system-stored-procedures/sp-fulltext-pendingchanges-transact-sql) ao atualizar a coluna de chave|Atualizar a coluna de chave de texto completo em uma linha de uma tabela de 2 linhas e executar sp_fulltext_pendingchanges.|As duas linhas aparecem.|Somente uma linha aparece.|  
|Funções embutidas|Funções embutidas com um operador de texto completo|Retorna uma mensagem de erro.|Retorna as linhas relevantes.|  
|[sp_fulltext_database](/sql/relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql)|Habilitar ou desabilitar pesquisa de texto completo usando sp_fulltext_database.|Nenhum resultado é retornado para consultas de texto completo. Se o texto completo estiver desabilitado para o banco de dados, não serão permitidas operações de texto completo.|Retorna resultados para consultas de texto completo e operações de texto completo permitidas, mesmo se o texto completo estiver desabilitado para o banco de dados.|  
|Palavras irrelevantes (stop words) específicas da localidade|Consulta variantes específicas de um idioma pai, como o belga francês e o Canadá francês.|Consultas as variantes específicas de inlocalização são processadas pelos componentes (separadores de palavras, lematizadores e palavras irrelevantes) de seu idioma pai. Por exemplo, os componentes de francês (França) são usados para analisar francês (Bélgica).|Você deve adicionar palavras irrelevantes explicitamente para cada identificador de localidade (LCID). Por exemplo, você precisaria especificar um LCID para Bélgica, Canadá e França.|  
|Processo de lematização do dicionário de sinônimos|Usando o dicionário de sinônimos e formas flexivas (lematização).|Uma palavra do dicionário de sinônimos é lematizada automaticamente depois de sua expansão.|Se você deseja a forma lematizada na expansão, precisará adicionar explicitamente a forma lematizada.|  
|Caminho de catálogo de texto completo e grupo de arquivos|Trabalhando com catálogos de texto completo.|Cada catálogo de texto completo tem um caminho físico e pertence a um grupo de arquivos. Ele é tratado como um arquivo de banco de dados.|Um catálogo de texto completo é um objeto virtual; ele não pertence a nenhum grupo de arquivos. Um catálogo de texto completo é um conceito lógico que faz referência a um grupo de índices de texto completo.<br /><br /> Observação: as [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] [!INCLUDE[tsql](../includes/tsql-md.md)] instruções DDL que especificam catálogos de texto completo funcionam corretamente.|  
|[sys.fulltext_catalogs](/sql/relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql)|Usando o caminho, data_space_id e file_id dessa exibição de catálogo.|Essas colunas retornam um valor específico.|Essas colunas retornam NULL porque o catálogo de texto completo não está mais localizado no sistema de arquivos.|  
|[sys.sysfulltextcatalogs](/sql/relational-databases/system-compatibility-views/sys-sysfulltextcatalogs-transact-sql)|Usando a coluna de caminho dessa tabela de sistema preterida.|Retorna o caminho do sistema de arquivos do catálogo de texto completo.|Retorna NULL porque o catálogo de texto completo não está mais localizado no sistema de arquivos.|  
|[sp_help_fulltext_catalogs](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql)<br /><br /> [sp_help_fulltext_catalogs_cursor](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql)|Usando a coluna PATH desses procedimentos armazenados preteridos.|Retorna o caminho do sistema de arquivos do catálogo de texto completo.|Retorna NULL porque o catálogo de texto completo não está mais localizado no sistema de arquivos.|  
|[sp_help_fulltext_catalog_components](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalog-components-transact-sql)|Usando sp_help_fulltext_catalog_components desse procedimento armazenado.|Retorna uma lista de todos os componentes (filtros, separadores de palavras e manipuladores de protocolo) usados em todos os catálogos de texto completo do banco de dados atual.|Retorna linhas vazias.|  
|[DATABASEPROPERTYEX](/sql/t-sql/functions/databasepropertyex-transact-sql)|Usando a propriedade **IsFullTextEnabled** .|A configuração **IsFullTextEnabled** indica se a pesquisa de texto completo está habilitada em um determinado banco de dados.|O valor dessa coluna não tem nenhum efeito. Os bancos de dados de usuário são sempre habilitados para pesquisa de texto completo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Alterações de comportamento na pesquisa de texto completo](../relational-databases/search/full-text-search.md)   
 [Pesquisa de texto completo](../relational-databases/search/full-text-search.md)  
  
  
