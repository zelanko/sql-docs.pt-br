---
title: Configurar e gerenciar separadores de palavras e lematizadores de pesquisa | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: search
ms.reviewer: ''
ms.suite: sql
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
caps.latest.revision: 89
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 40e307bd848dc71a1b48fc939bdbe207044b9d8a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="configure-and-manage-word-breakers-and-stemmers-for-search"></a>Configurar e gerenciar separadores de palavras e lematizadores de pesquisa
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Os separadores de palavras e os lematizadores executam a análise linguística em todos os dados indexados de texto completo. Análise linguística faz as duas coisas a seguir:

-   **Localizar os limites de palavra (quebra de palavras)**. O *separador de palavras* identifica palavras individuais determinando onde existem limites de palavra com base nas regras lexicais do idioma. Cada palavra (também conhecida como *token*) é inserida no índice de texto completo usando uma representação compactada para reduzir seu tamanho.

-   **Conjugar verbos (lematização)**. O *lematizador* gera formas flexionadas de uma palavra específica com base nas regras do idioma (por exemplo, “executando”, “executou” e “executor” são várias formas da palavra “executar”).

## <a name="word-breakers-and-stemmers-are-language-specific"></a>Os separadores de palavras e os lematizadores são específicos do idioma

Os separadores de palavras e os lematizadores são específicos de idioma, e as regras de análise linguística diferem conforme o idioma. Separadores de palavras específicos a um idioma tornam os termos resultantes mais precisos para esse idioma.

Para usar os separadores de palavras e lematizadores fornecidos para todos os idiomas aos quais o SQL Server dá suporte, normalmente não é necessário tomar nenhuma providência.

-   Se houver um separador de palavras para uma família de idiomas, mas não para um subidioma em particular, será usado o idioma principal. Por exemplo, o separador de palavras Francês é usado para tratar o texto em francês (Canadá).
-   Se não houver um separador de palavras disponível para um determinado idioma, será usado o separador de palavras neutro. Com ele, a separação das palavras é feita nos caracteres neutros, como espaços e marcas de pontuação.

## <a name="get-the-list-of-supported-languages"></a>Obter uma lista dos idiomas com suporte

Para ver a lista de idiomas aos quais a Pesquisa de Texto Completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte, use a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. A presença de um idioma nesta lista indica que o os separadores de palavras foram registrados para o idioma. 
  
```sql
SELECT * FROM sys.fulltext_languages
```

##  <a name="register"></a> Obter a lista de separadores de palavras registrados

Para que a Pesquisa de Texto Completo use os separadores de palavras de um idioma, eles devem ser registrados. Para separadores de palavras registrados, os recursos linguísticos associados – lematizadores, palavras de ruído (palavras irrelevantes) e arquivos de dicionário de sinônimos – também ficam disponíveis para operações de indexação e consulta de texto completo.

Para ver a lista de componentes do separador de palavras registrados, use a instrução a seguir.

```sql
EXEC sp_help_fulltext_system_components 'wordbreaker';  
GO  
```

Para obter opções adicionais e mais informações, consulte [sp_help_fulltext_system_components &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md).
 
## <a name="if-you-add-or-remove-a-word-breaker"></a>Se você adicionar ou remover um separador de palavras  
Se você adicionar, remover ou alterar um separador de palavras, precisará atualizar a lista de LCIDs (IDs de localidade) do Microsoft Windows que são suportadas para indexação e consulta de texto completo. Para obter mais informações, consulte [Exibir ou alterar filtros registrados e separadores de palavras](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).  
  
##  <a name="default"></a> Definir a opção de idioma de texto completo padrão  
 Em uma versão localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configura a opção **idioma de texto completo padrão** com o idioma do servidor caso exista uma correspondência apropriada. Para uma versão não localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a opção **idioma de texto completo padrão** estará em inglês.  
  
 Ao criar ou alterar um índice de texto completo, é possível especificar um idioma diferente para cada coluna indexada de texto completo. Se nenhum idioma for especificado para uma coluna, o padrão será o valor da opção de configuração **idioma de pesquisa de texto completo**.  
  
> [!NOTE]  
>  Todas as colunas listadas em uma única cláusula de função de consulta de texto completo devem usar o mesmo idioma, exceto se a opção LANGUAGE for especificada na consulta. O idioma usado para a coluna indexada de texto completo que está sendo consultada determina a análise linguística realizada nos argumentos dos predicados de consulta de texto completo ([CONTAINS](../../t-sql/queries/contains-transact-sql.md) e [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)) e das funções ([CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) e [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md)).  
  
##  <a name="lang"></a> Escolher o idioma de uma coluna indexada  
 Quando você cria um índice de texto completo, é recomendável especificar um idioma para cada coluna indexada. Se não for especificado um idioma para uma coluna, será usado o idioma padrão do sistema. O idioma de uma coluna determina que separador de palavras e que lematizador são usados para indexá-la. Além disso, o arquivo do dicionário de sinônimos do idioma será usado por consultas de texto completo na coluna.  
  
 Existem alguns aspectos que devem ser considerados na escolha do idioma da coluna para criar um índice de texto completo. Essas considerações estão relacionadas a como seu texto é transformado em token e, depois, indexado pelo Mecanismo de Texto Completo. Para obter mais informações, veja [Escolher um idioma ao criar um índice de texto completo](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
Para exibir o idioma do separador de palavras de colunas específicas, execute a seguinte instrução.
   
```sql 
SELECT 'language_id' AS "LCID" FROM sys.fulltext_index_columns;
```  

Para obter opções adicionais e mais informações, consulte [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md).

##  <a name="tshoot"></a> Solucionar problemas de erros de tempo limite na separação de palavras  
 Um erro de tempo limite na separação de palavras pode ocorrer em diversas situações. ou informações sobre estas situações e o que fazer em cada uma delas, consulte [MSSQLSERVER_30053](https://msdn.microsoft.com/en-us/library/cc879279.aspx).

### <a name="info-about-the-mssqlserver30053-error"></a>Informações sobre o erro MSSQLSERVER_30053
  
|Propriedade|Valor|
|-|-|
|Nome do produto|SQL Server|  
|ID do evento|30053|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|FTXT_QUERY_E_WORDBREAKINGTIMEOUT|  
|Texto da mensagem|Foi atingido o tempo limite de quebra de palavras para a cadeia de consulta de texto completo. O separador de palavras pode ter demorado para processar a cadeia de consulta de texto completo ou um grande número de consultas está em execução no servidor. Tente executar a consulta novamente com uma carga mais leve.|  
  
#### <a name="explanation"></a>Explicação  
 Um erro de tempo limite na separação de palavras pode ocorrer nas seguintes situações:  
  
-   O separador de palavras para o idioma da consulta está configurado incorretamente. Por exemplo, suas configurações de Registro estão incorretas.  
  
-   O separador de palavras funciona incorretamente em uma cadeia de consulta específica.  
  
-   O separador de palavras retorna uma quantidade excessiva de dados para uma cadeia de consulta específica. O excesso de dados é tratado como um ataque de saturação de buffer em potencial e desliga o processo de daemon de filtro (fdhost.exe) que hospeda os serviços de separação de palavras.  
  
-   A configuração do processo de daemon de filtro está incorreta.  
  
     A maior parte dos problemas comuns de configuração são vencimento de senha ou uma política de domínio que impede que a conta do daemon do filtro faça o logon.  
  
-   Uma carga de trabalho de consultas muito pesada está em execução na instância do servidor. Por exemplo, o separador de palavras demorou muito para processar a cadeia de consultas de texto completo ou um grande número de consultas está em execução no servidor. Observe que essa é a causa menos provável.  
  
#### <a name="user-action"></a>Ação do usuário  
 Selecione a ação do usuário apropriada à causa provável do tempo limite, da seguinte maneira:  
  
|Causa provável|Ação do usuário|  
|--------------------|-----------------|  
|O separador de palavras para o idioma da consulta está configurado incorretamente.|Se você estiver usando um separador de palavras de terceiros, ele poderá estar registrado incorretamente com o sistema operacional. Nesse caso, registre novamente o separador de palavras. Para obter mais informações, consulte [Reverter os separadores de palavras usados pela pesquisa para a versão anterior](revert-the-word-breakers-used-by-search-to-the-previous-version.md).|  
|O separador de palavras funciona incorretamente em uma cadeia de consulta específica.|Se o separador de palavras for suportado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], entre em contato com o Suporte e Atendimento ao Cliente Microsoft.|  
|O separador de palavras retorna uma quantidade excessiva de dados para uma cadeia de consulta específica.|Se o separador de palavras for suportado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], entre em contato com o Suporte e Atendimento ao Cliente Microsoft.|  
|A configuração do processo de daemon de filtro está incorreta.|Verifique se você está usando a senha atual e se uma política de domínio não está impedindo a conta do daemon de filtro de fazer logon.|  
|Uma carga de trabalho de consulta muito pesada está em execução na instância do servidor.|Tente executar a consulta novamente com uma carga mais leve.|  

##  <a name="impact"></a> Noções básicas sobre o impacto dos separadores de palavras atualizados  
 Cada versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente inclui novos separadores de palavras que possuem regras linguísticas melhores e mais precisas do que os separadores de palavras anteriores. O comportamento dos novos separadores de palavras pode ser ligeiramente diferente daquele dos separadores de palavras em índices de texto completo importados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
 
Isso é significativo se um catálogo de texto completo foi importado durante a atualização de um banco de dados para a versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Agora um ou mais dos idiomas usados pelos índices de texto completo no catálogo de texto completo podem ser associados aos novos separadores de palavras. Para obter mais informações, veja [Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  

## <a name="see-also"></a>Consulte Também  
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)    
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes (stoplists) para pesquisa de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 
  
