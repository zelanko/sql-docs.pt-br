---
title: Configurar e gerenciar separadores de palavras e lematizadores de pesquisa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- languages [full-text search]
- full-text search [SQL Server], stemmers
- linguistic analysis [full-text search]
- full-text indexes [SQL Server], linguistic analysis
- full-text search [SQL Server], word breakers
- default full-text language option
- stemmers [full-text search]
- conjugating verbs [full-text search]
- word breakers [full-text search]
ms.assetid: d4bdd16b-a2db-4101-a946-583d1c674229
caps.latest.revision: 88
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 4c3bfb07ca9730b8c03cb56f07464355c392bda6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130732"
---
# <a name="configure-and-manage-word-breakers-and-stemmers-for-search"></a>Configurar e gerenciar separadores de palavras e lematizadores de pesquisa
  Os separadores de palavras e os lematizadores executam a análise linguística em todos os dados indexados de texto completo. A análise linguística envolve a localização dos limites das palavras (separação de palavras) e a conjugação de verbos (lematização). Os separadores de palavras e os lematizadores são específicos de idioma, e as regras de análise linguística diferem conforme o idioma. Para um idioma específico, um *separador de palavras* identifica palavras individuais determinando em que existem limites de palavra com base nas regras lexicais do idioma. Cada palavra (também conhecida como *token*) é inserida no índice de texto completo usando uma representação compactada para reduzir seu tamanho. O *lematizador* gera formas flexionadas de uma palavra específica com base nas regras do idioma (por exemplo, “executando”, “executou” e “executor” são várias formas da palavra “executar”).  
  
 O uso de separadores de palavras específicos de idioma permite que os termos resultantes sejam mais precisos para o idioma em questão. Se houver um separador de palavras para uma família de idiomas, mas não para um subidioma em particular, será usado o idioma principal. Por exemplo, o separador de palavras Francês é usado para tratar o texto em francês (Canadá). Se não houver um separador de palavras disponível para um determinado idioma, será usado o separador de palavras neutro. Com ele, a separação das palavras é feita nos caracteres neutros, como espaços e marcas de pontuação.  
  
##  <a name="register"></a> Registrando separadores de palavras  
 Para que os separadores de palavras de um idioma possam ser usados, é necessário registrá-los. Nos separadores de palavras registrados, os recursos associados, como lematizadores, palavras de ruído (palavras irrelevantes) e arquivos de dicionário de sinônimos, também ficam disponíveis para operações de indexação e consulta de texto completo. Para exibir uma lista dos idiomas cujos separadores de palavras estão registrados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
 SELECT * FROM sys.fulltext_languages  
  
 Se você adicionar, remover ou alterar um separador de palavras, precisará atualizar a lista de LCIDs (IDs de localidade) do Microsoft Windows que são suportadas para indexação e consulta de texto completo. Para obter mais informações, consulte [Exibir ou alterar filtros registrados e separadores de palavras](view-or-change-registered-filters-and-word-breakers.md).  
  
##  <a name="default"></a> Definindo a opção de idioma de texto completo padrão  
 Para uma versão localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de configuração o `default full-text language` opção para o idioma do servidor caso exista uma correspondência apropriada. Para obter uma versão não localizada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o `default full-text language` opção é inglês.  
  
 Quando criar ou alterar um índice de texto completo, você pode especificar um idioma diferente para cada coluna indexada de texto completo. Se nenhum idioma for especificado para uma coluna, o padrão será o valor da opção de configuração `default full-text language`.  
  
> [!NOTE]  
>  Todas as colunas listadas em uma única cláusula de função de consulta de texto completo devem usar o mesmo idioma, exceto se a opção LANGUAGE for especificada na consulta. O idioma usado para a coluna indexada de texto completo que está sendo consultada determina a análise linguística realizada nos argumentos dos predicados de consulta de texto completo ([CONTAINS](/sql/t-sql/queries/contains-transact-sql) e [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)) e das funções ([CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) e [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql)).  
  
##  <a name="lang"></a> Escolhendo o idioma para uma coluna indexada  
 Quando você cria um índice de texto completo, é recomendável especificar um idioma para cada coluna indexada. Se não for especificado um idioma para uma coluna, será usado o idioma padrão do sistema. O idioma de uma coluna determina que separador de palavras e que lematizador são usados para indexá-la. Além disso, o arquivo do dicionário de sinônimos do idioma será usado por consultas de texto completo na coluna.  
  
 Existem alguns aspectos que devem ser considerados na escolha do idioma da coluna para criar um índice de texto completo. Essas considerações estão relacionadas a como seu texto é transformado em token e, depois, indexado pelo Mecanismo de Texto Completo. Para obter mais informações, veja [Escolher um idioma ao criar um índice de texto completo](choose-a-language-when-creating-a-full-text-index.md).  
  
 **Para exibir o idioma do separador de palavras de uma coluna**  
  
-   [Administrar índices de texto completo](../indexes/indexes.md)  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)  
  
    ```  
    SELECT 'language_id' AS "LCID" FROM sys.fulltext_index_columns;  
    ```  
  
##  <a name="info"></a> Obtendo informações sobre separadores de palavras  
 **Exibindo o resultado da geração de tokens de uma combinação de separador, dicionário de sinônimos e lista de palavras irrelevantes do word**  
  
-   [sys.dm_fts_parser &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql).  
  
 **Para retornar informações sobre os separadores de palavras registrados**  
  
-   [sp_help_fulltext_system_components &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql)  
  
##  <a name="tshoot"></a> Solucionando problemas de erros de tempo limite de separação de palavras  
 Um erro de tempo limite na separação de palavras pode ocorrer em diversas situações. Para obter informações sobre estas situações e o que fazer em cada uma delas, veja [MSSQLSERVER_30053](../errors-events/mssqlserver-30053-database-engine-error.md).  
  
##  <a name="impact"></a> Noções básicas sobre o impacto dos novos separadores  
 Cada versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente inclui novos separadores de palavras que possuem regras linguísticas melhores e mais precisas do que os separadores de palavras anteriores. O comportamento dos novos separadores de palavras pode ser ligeiramente diferente daquele dos separadores de palavras em índices de texto completo importados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso é significativo se um catálogo de texto completo foi importado durante a atualização de um banco de dados para a versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Agora um ou mais dos idiomas usados pelos índices de texto completo no catálogo de texto completo podem ser associados aos novos separadores de palavras. Para obter mais informações, veja [Atualizar pesquisa de texto completo](upgrade-full-text-search.md).  
  
 Para obter uma lista completa de todos os separadores de palavra, veja [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql).  
  
## <a name="see-also"></a>Consulte também  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)   
 [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)   
 [Configurar e gerenciar palavras irrelevantes (stop words) e listas de palavras irrelevantes (stoplists) para a pesquisa de texto completo](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [Atualizar pesquisa de texto completo](upgrade-full-text-search.md)  
  
  
