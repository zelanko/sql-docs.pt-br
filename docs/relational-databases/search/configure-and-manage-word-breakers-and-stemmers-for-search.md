---
title: "Configurar e gerenciar separadores de palavras e lematizadores de pesquisa | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "idiomas [pesquisa de texto completo]"
  - "pesquisa de texto completo [SQL Server], lematizadores"
  - "análise linguística [pesquisa de texto completo]"
  - "índices de texto completo [SQL Server], análise linguística"
  - "pesquisa de texto completo [SQL Server], separadores de palavras"
  - "opção default full-text language"
  - "lematizadores [pesquisa de texto completo]"
  - "conjugando verbos [pesquisa de texto completo]"
  - "separadores de palavras [pesquisa de texto completo]"
ms.assetid: d4bdd16b-a2db-4101-a946-583d1c674229
caps.latest.revision: 89
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 88
---
# Configurar e gerenciar separadores de palavras e lematizadores de pesquisa
  Os separadores de palavras e os lematizadores executam a análise linguística em todos os dados indexados de texto completo. A análise linguística envolve a localização dos limites das palavras (separação de palavras) e a conjugação de verbos (lematização). Os separadores de palavras e os lematizadores são específicos de idioma, e as regras de análise linguística diferem conforme o idioma. Para um idioma específico, um *separador de palavras* identifica palavras individuais determinando em que existem limites de palavra com base nas regras lexicais do idioma. Cada palavra (também conhecida como *token*) é inserida no índice de texto completo usando uma representação compactada para reduzir seu tamanho. O *lematizador* gera formas flexionadas de uma palavra específica com base nas regras do idioma (por exemplo, “executando”, “executou” e “executor” são várias formas da palavra “executar”).  
  
 O uso de separadores de palavras específicos de idioma permite que os termos resultantes sejam mais precisos para o idioma em questão. Se houver um separador de palavras para uma família de idiomas, mas não para um subidioma em particular, será usado o idioma principal. Por exemplo, o separador de palavras Francês é usado para tratar o texto em francês (Canadá). Se não houver um separador de palavras disponível para um determinado idioma, será usado o separador de palavras neutro. Com ele, a separação das palavras é feita nos caracteres neutros, como espaços e marcas de pontuação.  
  
##  <a name="register"></a> Registrando separadores de palavras  
 Para que os separadores de palavras de um idioma possam ser usados, é necessário registrá-los. Nos separadores de palavras registrados, os recursos associados, como lematizadores, palavras de ruído (palavras irrelevantes) e arquivos de dicionário de sinônimos, também ficam disponíveis para operações de indexação e consulta de texto completo. Para exibir uma lista dos idiomas cujos separadores de palavras estão registrados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
 SELECT * FROM sys.fulltext_languages  
  
 Se você adicionar, remover ou alterar um separador de palavras, precisará atualizar a lista de LCIDs (IDs de localidade) do Microsoft Windows que são suportadas para indexação e consulta de texto completo. Para obter mais informações, consulte [View or Change Registered Filters and Word Breakers](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).  
  
##  <a name="default"></a> Definindo a opção de idioma de texto completo padrão  
 Em uma versão localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configura a opção **idioma de texto completo padrão** com o idioma do servidor caso exista uma correspondência apropriada. Para uma versão não localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a opção **idioma de texto completo padrão** estará em inglês.  
  
 Quando criar ou alterar um índice de texto completo, você pode especificar um idioma diferente para cada coluna indexada de texto completo. Se nenhum idioma for especificado para uma coluna, o padrão será o valor da opção de configuração **idioma de pesquisa de texto completo**.  
  
> [!NOTE]  
>  Todas as colunas listadas em uma única cláusula de função de consulta de texto completo devem usar o mesmo idioma, exceto se a opção LANGUAGE for especificada na consulta. O idioma usado para a coluna indexada de texto completo que está sendo consultada determina a análise linguística realizada nos argumentos dos predicados de consulta de texto completo ([CONTAINS](../../t-sql/queries/contains-transact-sql.md) e [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)) e das funções ([CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) e [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md)).  
  
##  <a name="lang"></a> Escolhendo o idioma para uma coluna indexada  
 Quando você cria um índice de texto completo, é recomendável especificar um idioma para cada coluna indexada. Se não for especificado um idioma para uma coluna, será usado o idioma padrão do sistema. O idioma de uma coluna determina que separador de palavras e que lematizador são usados para indexá-la. Além disso, o arquivo do dicionário de sinônimos do idioma será usado por consultas de texto completo na coluna.  
  
 Existem alguns aspectos que devem ser considerados na escolha do idioma da coluna para criar um índice de texto completo. Essas considerações estão relacionadas a como seu texto é transformado em token e, depois, indexado pelo Mecanismo de Texto Completo. Para obter mais informações, veja [Escolher um idioma ao criar um índice de texto completo](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
 **Para exibir o idioma do separador de palavras de uma coluna**  
  
-   [Gerenciar índices de texto completo](../Topic/Manage%20Full-Text%20Indexes.md)  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
  
    ```  
    SELECT 'language_id' AS "LCID" FROM sys.fulltext_index_columns;  
    ```  
  
##  <a name="info"></a> Obtendo informações sobre separadores de palavras  
 **Exibindo o resultado da geração de tokens de uma combinação de separador de palavras, dicionário de sinônimos e lista de palavras irrelevantes**  
  
-   [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md).  
  
 **Para retornar informações sobre os separadores de palavras registrados**  
  
-   [sp_help_fulltext_system_components &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
  
##  <a name="tshoot"></a> Solucionando problemas de erros de tempo limite de separação de palavras  
 Um erro de tempo limite na separação de palavras pode ocorrer em diversas situações. Para obter informações sobre estas situações e o que fazer em cada uma delas, veja [MSSQLSERVER_30053](../Topic/MSSQLSERVER_30053.md).  
  
##  <a name="impact"></a> Noções sobre o impacto dos novos separadores de palavras  
 Cada versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente inclui novos separadores de palavras que possuem regras linguísticas melhores e mais precisas do que os separadores de palavras anteriores. O comportamento dos novos separadores de palavras pode ser ligeiramente diferente daquele dos separadores de palavras em índices de texto completo importados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso é significativo se um catálogo de texto completo foi importado durante a atualização de um banco de dados para a versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Agora um ou mais dos idiomas usados pelos índices de texto completo no catálogo de texto completo podem ser associados aos novos separadores de palavras. Para obter mais informações, veja [Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  
 Para obter uma lista completa de todos os separadores de palavra, veja [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
  
## Consulte também  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)   
 [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes (stoplists) para pesquisa de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md)  
  
  