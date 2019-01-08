---
title: Consulta com a pesquisa de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- queries [full-text search], about full-text queries
- queries [full-text search], predicates
- full-text queries [SQL Server], about full-text queries
- full-text search [SQL Server], querying SQL Server
- full-text queries [SQL Server]
- queries [full-text search], functions
ms.assetid: 7624ba76-594b-4be5-ac10-c3ac4a3529bd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 244161359910896533a1d7179f2ce80b5cb03d86
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749420"
---
# <a name="query-with-full-text-search"></a>Query with Full-Text Search
  Para definir consultas de texto completo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa os predicados de texto completo (CONTAINS e FREETEXT) e as funções (CONTAINSTABLE e FREETEXTTABLE). Elas dão suporte à avançada sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] que comporta uma variedade de formas de termos de consulta. Para gravar consultas de texto completo, você deve saber quando e como usar esses predicados e funções.  
  
##  <a name="OV_ft_predicates"></a> Visão geral de texto completo predicados (CONTAINS e FREETEXT)  
 Os predicados CONTAINS e FREETEXT retornam um valor TRUE ou FALSE. Eles podem ser usados somente para especificar critérios de seleção para determinar se uma dada linha corresponde à consulta de texto completo. As linhas correspondentes são retornadas no conjunto de resultados. CONTAINS e FREETEXT são especificados na cláusula WHERE ou HAVING de uma instrução SELECT. Eles podem ser combinados com qualquer dos outros predicados [!INCLUDE[tsql](../../includes/tsql-md.md)] , como LIKE e BETWEEN.  
  
> [!NOTE]  
>  Para obter informações sobre a sintaxe e os argumentos desses predicados, veja [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql) e [FREETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql).  
  
 Ao usar CONTAINS ou FREETEXT, você pode especificar se uma única coluna, uma lista de colunas ou todas as colunas da tabela devem ser pesquisadas. Se preferir, você pode especificar o idioma cujos recursos serão usados por uma dada consulta de texto completo para quebra de palavras e lematização, pesquisas no dicionário de sinônimos e remoção de palavras de ruído.  
  
 CONTAINS e FREETEXT são úteis para diferentes tipos de correspondências, como segue:  
  
-   Use CONTAINS (ou CONTAINSTABLE) para obter correspondências precisas ou difusas (menos precisas) para palavras e frases únicas, a proximidade entre as palavras dentro de uma determinada distância ou correspondências ponderadas. Ao usar CONTAINS, você deve especificar pelo menos um critério de pesquisa que especifique o texto procurado e as condições que determinam correspondências.  
  
     Você pode usar uma operação lógica entre condições de pesquisa. Para obter mais informações, consulte [usando operadores boolianos – AND, OR e NOT (em CONTAINS e CONTAINSTABLE)](#Using_Boolean_Operators), mais adiante neste tópico.  
  
-   Use FREETEXT (ou FREETEXTTABLE) para fazer a correspondência de significado, mas não da frase exata, de palavras, frases ou sentenças especificadas (a *cadeia de caracteres de texto livre*). As correspondências serão geradas se qualquer termo ou forma de qualquer termo for encontrada no índice de texto completo de uma coluna especificada.  
  
 É possível usar um nome de quatro partes no predicado CONTAINS ou FREETEXT para consultar colunas indexadas de texto completo das tabelas de destino em um servidor vinculado. Para preparar um servidor remoto para receber consultas de texto completo, crie um índice de texto completo nas tabelas e colunas de destino no servidor remoto e, em seguida, adicione o servidor remoto como um servidor vinculado.  
  
> [!NOTE]  
>  Predicados de texto completo não são permitidos na [Cláusula OUTPUT](/sql/t-sql/queries/output-clause-transact-sql) quando o nível de compatibilidade do banco de dados está definido como 100.  
  
 
  
### <a name="examples"></a>Exemplos  
  
#### <a name="a-using-contains-with-simpleterm"></a>A. Usando CONTAINS com <simple_term>  
 O exemplo a seguir localiza todos os produtos com um preço de `$80.99` contendo a palavra `"Mountain"`.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Name, ListPrice  
FROM Production.Product  
WHERE ListPrice = 80.99  
   AND CONTAINS(Name, 'Mountain')  
GO  
```  
  
#### <a name="b-using-freetext-to-search-for-words-containing-specified-character-values"></a>b. Usando FREETEXT para pesquisar palavras que contêm valores de caracteres especificados  
 As pesquisas de exemplo a seguir para todos os documentos que contêm as palavras relacionadas a componentes vitais, de segurança.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components')  
GO  
```  
  
 
  
##  <a name="OV_ft_functions_CONTAINSTABLE_FREETEXTTABLE"></a> Visão geral das funções de texto completo (CONTAINSTABLE e FREETEXTTABLE)  
 As funções CONTAINSTABLE e FREETEXTTABLE são referenciadas como um nome de tabela comum na cláusula FROM de uma instrução SELECT. Elas retornam uma tabela de zero, uma ou mais linhas que correspondem à consulta de texto completo. A tabela retornada contém somente as linhas da tabela base que atendem aos critérios de seleção especificados no critério de pesquisa de texto completo da função.  
  
> [!NOTE]  
>  Para obter informações sobre a sintaxe e os argumentos dessas funções, veja [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql) e [FREETEXTTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql).  
  
 As consultas que usam uma dessas funções retornam um valor de classificação de relevância (RANK) e uma chave de texto completo (KEY) para cada linha, da seguinte maneira:  
  
-   Coluna KEY  
  
     A coluna KEY retorna valores exclusivos das linhas retornadas. A coluna KEY pode ser usada para especificar critérios de seleção.  
  
-   Coluna RANK  
  
     A coluna RANK retorna um *valor de classificação* para cada linha que indica o grau de correspondência da linha com os critérios de seleção. Quanto mais alto o valor de classificação do texto ou documento em uma linha, mais relevante será a linha para a consulta de texto completo especificada. Observe que diferentes linhas podem ter a mesma classificação. É possível limitar o número de correspondências a serem retornadas especificando o parâmetro opcional *top_n_by_rank* . Para obter mais informações, veja [Limitar resultados da pesquisa com RANK](limit-search-results-with-rank.md).  
  
 Ao usar uma dessas funções, você deve especificar a tabela base que deve ser objeto da pesquisa de texto completo. Assim como nos predicados, você pode especificar uma única coluna, uma lista de colunas ou todas as colunas da tabela a ser pesquisada e, se preferir, o idioma cujos recursos serão usados por uma dada consulta de texto completo.  
  
 CONTAINSTABLE é útil para os mesmos tipos de correspondências que CONTAINS, e FREETEXTTABLE é útil para os mesmos tipos de correspondências que FREETEXT. Para obter mais informações, veja [Visão geral dos predicados de texto completo (CONTAINS e FREETEXT)](#OV_ft_predicates), acima neste tópico. Ao executar consultas que usam as funções CONTAINSTABLE e FREETEXTTABLE, você deve associar explicitamente as linhas retornadas às linhas na tabela base do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Normalmente, o resultado de CONTAINSTABLE ou FREETEXTTABLE precisa ser associado à tabela base. Nesses casos, você precisa saber o nome da coluna de chave exclusiva. Esta coluna, que ocorre em todas as tabelas habilitadas para texto completo, é usada para impor linhas exclusivas da tabela (a *coluna de chave**exclusiva*). Para obter mais informações, veja [Gerenciar índices de texto completo](../indexes/indexes.md).  
  
 
  
### <a name="examples"></a>Exemplos  
  
#### <a name="a-using-containstable"></a>A. Usando CONTAINSTABLE  
 O exemplo a seguir retorna a ID de descrição e a descrição de todos os produtos para os quais a coluna **Description** contém a palavra “aluminum” ao lado da palavra “light” ou “lightweight”. Apenas as linhas com valor de classificação 2 ou superior são retornadas.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)'  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 2  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
#### <a name="b-using-freetexttable"></a>b. Usando FREETEXTTABLE  
 O exemplo a seguir estende uma consulta FREETEXTTABLE para retornar primeiro as linhas com classificação mais alta e adicionar a classificação de cada linha à lista de seleção. Para especificar a consulta, você deve saber que **ProductDescriptionID** é a coluna de chave exclusiva para o `ProductDescription` tabela.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 Esta é uma extensão da mesma consulta que retorna apenas as linhas com um valor de classificação 10 ou maior:  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK >= 10  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 
  
##  <a name="Using_Boolean_Operators"></a> Usando operadores boolianos – e, OR e não – em CONTAINS e CONTAINSTABLE  
 O predicado CONTAINS e a função CONTAINSTABLE usam as mesmas condições de pesquisa. Os dois permitem combinar vários termos de pesquisa usando operadores boolianos – AND, OR e não-para executar operações lógicas. Você pode usar AND, por exemplo, para localizar linhas que contêm "expresso" e "rosca". Você pode usar AND NOT, por exemplo, para localizar as linhas que contêm "rosca" mas que não contêm "cream cheese".  
  
> [!NOTE]  
>  Por outro lado, FREETEXT e FREETEXTTABLE tratam os termos boolianos como palavras a serem pesquisadas.  
  
 Para obter mais informações sobre como combinar CONTAINS com outros predicados que usam os operadores lógicos AND, OR e NOT, veja [Critério de pesquisa &#40;Transact-SQL&#41;](/sql/t-sql/queries/search-condition-transact-sql).  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir usa a tabela ProductDescription do banco de dados [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] . A consulta usa o predicado CONTAINS para procurar descrições nas quais a ID de descrição não é igual a 5 e a descrição contém as palavras "Aluminum" e "spindle". O critério de pesquisa usa o operador booliano AND.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'aluminum AND spindle')  
GO  
```  
  
 
  
##  <a name="Additional_Considerations"></a> Considerações adicionais para consultas de texto completo  
 Ao escrever consultas de texto completo, considere também o seguinte:  
  
-   A opção LANGUAGE  
  
     Muitos termos de consulta dependem bastante do comportamento do separador de palavras. Para assegurar que você use o separador de palavras (e lematizador) e o arquivo de dicionário de sinônimos corretos, é recomendável especificar a opção LANGUAGE. Para obter mais informações, veja [Escolher um idioma ao criar um índice de texto completo](choose-a-language-when-creating-a-full-text-index.md).  
  
-   Palavras irrelevantes  
  
     Ao definir uma consulta de texto completo, o Mecanismo de Texto Completo descarta as palavras irrelevantes (também chamadas de palavras de ruído) dos critérios de pesquisa. Palavras irrelevantes são palavras como "um", "e", "é" ou "o(s)/a(s)", que podem ocorrer com frequência, mas normalmente não ajudam na pesquisa de um determinado texto. As palavras irrelevantes são relacionadas em uma lista de palavras irrelevantes (stoplist). Cada índice de texto completo é associado a uma lista de palavras irrelevantes específica, que determina quais palavras irrelevantes são omitidas da consulta ou do índice no momento da indexação. Para obter mais informações, veja [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](full-text-search.md).  
  
-   O dicionário de sinônimos  
  
     As consultas FREETEXT e FREETEXTTABLE usam o dicionário de sinônimos por padrão. CONTAINS e CONTAINSTABLE suportam um argumento THESAURUS opcional.  
  
-   Diferenciação de maiúsculas e minúsculas  
  
     As consultas de pesquisa de texto completo não diferenciam maiúsculas de minúsculas. No entanto, em japonês há várias ortografias fonéticas em que o conceito de normalização ortográfica é parecido à não diferenciação de maiúsculas e minúsculas (por exemplo, kana = não diferenciação). Esse tipo de normalização ortográfica não tem suporte.  
  

  
##  <a name="varbinary"></a> Consultando varbinary (max) e colunas de xml  
 Se uma coluna `varbinary(max)`, `varbinary` ou `xml` tiver um índice de texto completo, poderá ser consultada usando os predicados (CONTAINS e FREETEXT) e as funções (CONTAINSTABLE e FREETEXTTABLE) de texto completo, como qualquer outra coluna indexada de texto completo.  
  
> [!IMPORTANT]  
>  A pesquisa de texto completo também funciona com colunas de imagem. No entanto, o tipo de dados `image` será removido em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esse tipo de dados em um novo trabalho de desenvolvimento e planeje modificar os aplicativos que o utilizam. Use o tipo de dados `varbinary(max)` em vez disso.  
  
### <a name="varbinarymax-or-varbinary-data"></a>Dados varbinary (max) ou varbinary  
 Uma única coluna `varbinary(max)` ou `varbinary` pode armazenar muitos tipos de documentos. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a qualquer tipo de documento para o qual um filtro está instalado e disponível no sistema operacional. O tipo de cada documento é identificado pela extensão de arquivo do documento. Por exemplo, no caso de uma extensão de arquivo .doc, a pesquisa de texto completo usa o filtro que dá suporte a documentos do Microsoft Word. Para obter uma lista dos tipos de documento disponíveis, veja a exibição de catálogo [sys.fulltext_document_types](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql) .  
  
 Observe que o Mecanismo de Texto Completo pode aproveitar os filtros existentes instalados no sistema operacional. Para que você possa usar filtros do sistema operacional, separadores de palavras e lematizadores, carregue-os na instância do servidor da seguinte maneira:  
  
```  
EXEC sp_fulltext_service @action='load_os_resources', @value=1  
```  
  
 Para criar um índice de texto completo em uma coluna `varbinary(max)`, o Mecanismo de Texto Completo precisa de acesso às extensões de arquivo dos documentos na coluna `varbinary(max)`. Esta informação deve ser armazenada em uma coluna de tabela, chamada de coluna de tipo, que deve estar associada à coluna `varbinary(max)` no índice de texto completo. Ao indexar um documento, o Mecanismo de Texto Completo utiliza a extensão de arquivo na coluna de tipo para identificar o filtro a ser usado.  
  
 
  
### <a name="xml-data"></a>Dados xml  
 Uma coluna de tipo de dados `xml` armazena apenas fragmentos e documentos XML, e somente o filtro XML é usado para os documentos. Portanto, uma coluna de tipo é desnecessária. Em colunas `xml`, o índice de texto completo indexa o conteúdo dos elementos XML, mas ignora a marcação XML. Os valores de atributos são indexados como texto completo, a menos que sejam valores numéricos. Marcas de elemento são usadas como limites do token. Há suporte a fragmentos e documentos XML ou HTML bem formados que contêm vários idiomas.  
  
 Para obter mais informações sobre como fazer consultas em uma `xml` coluna, consulte [Use a pesquisa de texto completo com colunas XML](../xml/use-full-text-search-with-xml-columns.md).  
  
 
  
##  <a name="supported"></a> Formatos suportados de termos de consulta  
 Esta seção resume o suporte fornecido em cada formato de consulta por predicados de texto completo e funções com valores de conjunto de linhas.  
  
> [!NOTE]  
>  Para obter a sintaxe um determinado termo da consulta, clique nos links correspondentes na coluna **Com suporte por** da tabela a seguir.  
  
|Formato de termo de consulta|Descrição|Com suporte por|  
|----------------------|-----------------|------------------|  
|Uma ou mais palavras ou frases específicas (*termo simples*)|Na pesquisa de texto completo, uma palavra (ou *token*) é uma cadeia de caracteres cujos limites são identificados pelos separadores de palavras apropriados, seguindo as regras linguísticas do idioma especificado. Uma frase válida consiste em várias palavras, com ou sem sinais de pontuação entre elas.<br /><br /> Por exemplo, "croissant" é uma palavra e "caf?? com leite"é uma frase. Palavras e frases como essas são chamadas de termos simples.<br /><br /> Para obter mais informações, veja [Procurando uma palavra ou frase específica (termo simples)](#Simple_Term), mais adiante neste tópico.|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) e [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) procuram uma correspondência exata da frase.<br /><br /> [FREETEXT](/sql/t-sql/queries/freetext-transact-sql) e [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) desmembram a frase em palavras separadas.|  
|Uma palavra ou frase na qual as palavras começam com o texto especificado (*termo de prefixo*)|Um termo de prefixo refere-se a uma cadeia de caracteres colocada na frente de uma palavra para gerar uma palavra derivada ou uma forma flexionada.<br /><br /> Para um único termo de prefixo, qualquer palavra que comece com o termo especificado fará parte do conjunto de resultados. Por exemplo, o termo "auto*" retorna "automático", "automóvel" e assim por diante.<br /><br /> Para uma frase, cada palavra é considerada um termo de prefixo. Por exemplo, o termo “tran auto\*” corresponde a “transmissão automática” e “transdutor de automóvel”, mas não corresponde a “transmissão de motor automática”.<br /><br /> Para obter mais informações, veja [Fazendo pesquisas de prefixo (termo de prefixo)](#Prefix_Term), mais adiante neste tópico.|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) e [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
|As formas flexionadas de uma palavra específica (*geração termo flexionada*)|As formas flexionadas são os diferentes tempos e conjugações de um verbo ou as formas singular e plural de um substantivo. Por exemplo, procure a forma flexionada da palavra "dirigir". Se várias linhas da tabela contivessem as palavras "dirigir", "dirige", "dirigiu", "dirigindo" e "dirigido", todas elas fariam parte do conjunto de resultados, pois cada uma delas seria uma flexão gerada da palavra dirigir.<br /><br /> Para obter mais informações, veja [Pesquisando a forma flexionada de uma palavra específica (termo de geração)](#Inflectional_Generation_Term), mais adiante neste tópico.|Por padrão,[FREETEXT](/sql/t-sql/queries/freetext-transact-sql) e [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) procuram termos flexionados de todas as palavras especificadas.<br /><br /> [CONTAINS](/sql/t-sql/queries/contains-transact-sql) e [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) dão suporte a um argumento INFLECTIONAL opcional.|  
|Sinônimos de uma palavra específica (*termo de geração – dicionário de sinônimos*)|Um dicionário de sinônimos define sinônimos especificados pelo usuário para os termos. Por exemplo, se uma entrada, "{carro, automóvel, caminhão, van}", for adicionada ao dicionário de sinônimos, será possível pesquisar o sinônimo da palavra "carro". Todas as linhas da tabela consultada que contiverem as palavras "automóvel", "caminhão", "van" ou "carro" serão exibidas no conjunto de resultados, pois cada uma dessas palavras pertence a um conjunto de expansão de sinônimos contendo a palavra "carro".<br /><br /> Para obter informações sobre a estrutura dos arquivos de dicionário de sinônimos, veja [Configurar e gerenciar arquivos de dicionário de sinônimos para a Pesquisa de Texto Completo](configure-and-manage-thesaurus-files-for-full-text-search.md).|[FREETEXT](/sql/t-sql/queries/freetext-transact-sql) e [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) usam o dicionário de sinônimos por padrão.<br /><br /> [CONTAINS](/sql/t-sql/queries/contains-transact-sql) e [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) dão suporte a um argumento THESAURUS opcional.|  
|Uma palavra ou frase perto de outra palavra ou frase (*termo de proximidade*).|Um termo de proximidade indica palavras ou frases que estão perto uma das outras. Você também pode especificar o número máximo de termos não relacionados à pesquisa que separam o primeiro e o último termo de pesquisa. Além disso, você pode pesquisar palavras ou frases em qualquer ordem, ou na ordem em que as especificar.<br /><br /> Por exemplo, você quer localizar as linhas em que a palavra "gelo" esteja perto de "hóquei" ou em que a frase "patinação no gelo" esteja perto da frase "hóquei no gelo".<br /><br /> Para obter mais informações, veja [Procurar palavras perto de outra palavra com NEAR](search-for-words-close-to-another-word-with-near.md).|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) e [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
|Palavras ou frases que usam valores ponderados (*termo ponderado*)|Um valor de ponderação que indica o grau de importância de cada palavra e frase em um conjunto de palavras e frases. Um valor ponderado de 0,0 é o mais baixo e um valor ponderado de 1,0 é o mais alto.<br /><br /> Por exemplo, em uma consulta que pesquisa vários termos, é possível atribuir a cada palavra da pesquisa um valor equilibrado indicando sua importância com relação às demais palavras da pesquisa. O resultado desse tipo de consulta retorna primeiro as linhas mais relevantes, de acordo com o peso relativo atribuído às palavras da pesquisa. Os conjuntos de resultados contêm documentos ou linhas que, por sua vez, contêm qualquer um dos termos especificados (ou conteúdo entre eles); todavia, alguns resultados serão considerados mais relevantes do que outros devido à variação dos valores ponderados associados aos diferentes termos de pesquisa.<br /><br /> Para obter mais informações, veja [Pesquisando palavras ou frases usando valores ponderados (termo ponderado)](#Weighted_Term), mais adiante neste tópico.|[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
  

  
###  <a name="Simple_Term"></a> Procurando uma palavra ou frase (termo simples) específica  
 Você pode usar [CONTAINS](/sql/t-sql/queries/contains-transact-sql), [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql), [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)ou [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) para pesquisar uma tabela para uma frase específica. Por exemplo, para pesquisar a tabela `ProductReview` no banco de dados [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] e localizar todos os comentários sobre um produto com a frase "curva de aprendizado", use o predicado CONTAINS, como segue:  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments, '"learning curve"')  
GO  
```  
  
 O critério de pesquisa, nesse caso, "curva de aprendizado", pode ser bastante complexo, podendo consistir em um ou mais termos.  
  
 
  
###  <a name="Prefix_Term"></a> Executando pesquisas de prefixo (termo de prefixo)  
 Você pode usar [CONTAINS](/sql/t-sql/queries/contains-transact-sql) ou [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) para procurar palavras ou frases com um prefixo especificado. Todas as entradas na coluna que contêm o texto que começa com o prefixo especificado são retornadas. Por exemplo, para procurar todas as linhas que contêm o prefixo `top`-, como em `top``ple`, `top``ping`e `top`. A consulta parece com:  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Description, ProductDescriptionID  
FROM Production.ProductDescription  
WHERE CONTAINS (Description, '"top*"' )  
GO  
```  
  
 Todo texto que corresponder ao texto especificado antes do asterisco (*) será retornado. Se o texto e o asterisco não forem delimitados por aspas duplas, como em `CONTAINS (DESCRIPTION, 'top*')`, a pesquisa de texto completo não considerará o asterisco como sendo um curinga.  
  
 Quando o termo de prefixo for uma frase, todos os tokens que constituírem a frase serão considerados termos de prefixo separados. Todas as linhas que têm palavras que começam com os termos de prefixo serão retornadas. Por exemplo, o termo de prefixo “pão light*” encontrará linhas com o texto de “pãozinho light” ou “pão light”, mas não retornará “pão torrado light”.  
  
 
  
###  <a name="Inflectional_Generation_Term"></a> Pesquisando formas flexionadas de uma palavra específica (termo de geração)  
 Você pode usar [CONTAINS](/sql/t-sql/queries/contains-transact-sql), [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql), [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)ou [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) para procurar todos os diferentes tempos e conjugações de um verbo ou ambas as formas, singular e plural, de um substantivo (uma pesquisa flexionada) ou sinônimos de uma palavra específica (uma pesquisa de dicionário de sinônimos).  
  
 O exemplo a seguir pesquisa qualquer forma de “foot" ("foot", "feet" e assim por diante) na coluna `Comments` da tabela `ProductReview` do banco de dados `AdventureWorks` .  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Comments, ReviewerName  
FROM Production.ProductReview  
WHERE CONTAINS (Comments, 'FORMSOF(INFLECTIONAL, "foot")')  
GO  
```  
  
> [!NOTE]  
>  A pesquisa de texto completo usa lematizadores, que permitem que você pesquise os diversos tempos e conjugações de um verbo, ou as formas singular e plural de um substantivo. Para obter mais informações sobre lematizadores, veja [Configurar e gerenciar separadores de palavras e lematizadores para pesquisa](configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  

  
###  <a name="Weighted_Term"></a> Pesquisando palavras ou frases usando valores ponderados (termo ponderado)  
 Você pode usar [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) para procurar palavras ou frases e especificar um valor ponderado. A ponderação, medida como um número de 0,0 a 1,0, indica a importância de cada palavra e frase em um conjunto de palavras e frases. Um peso 0,0 é o mais baixo, e um peso 1,0 é o mais alto.  
  
 O exemplo a seguir mostra uma consulta que procura todos os endereços de clientes usando pesos, em que qualquer texto que comece com a cadeia de caracteres "Bay" tem também "Street" ou "View". Os resultados dão uma classificação mais alta a essas linhas que contêm mais das palavras especificadas.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT AddressLine1, KEY_TBL.RANK   
FROM Person.Address AS Address INNER JOIN  
CONTAINSTABLE(Person.Address, AddressLine1, 'ISABOUT ("Bay*",   
         Street WEIGHT(0.9),   
         View WEIGHT(0.1)  
         ) ' ) AS KEY_TBL  
ON Address.AddressID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 Um termo ponderado pode ser usado junto com qualquer termo simples, termo de prefixo, termo de geração ou termo de proximidade.  
  

  
##  <a name="tokens"></a> Exibindo o resultado da geração de tokens de um separador de palavras, dicionário de sinônimos e combinação de lista de palavras irrelevantes  
 Depois de aplicar determinada combinação de separador de palavras, dicionário de sinônimos e lista de palavras irrelevantes a uma entrada de cadeia de caracteres de consulta, você poderá exibir o resultado da geração de tokens usando a exibição de gerenciamento dinâmico **sys.dm_fts_parser**. Para obter mais informações, veja [sys.dm_fts_parser &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql).  
  
 
  
## <a name="see-also"></a>Consulte também  
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [FREETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql)   
 [Criar consultas de pesquisa de texto completo &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md)   
 [Melhorar o desempenho de consultas de texto completo](improve-the-performance-of-full-text-queries.md)  
  
  
