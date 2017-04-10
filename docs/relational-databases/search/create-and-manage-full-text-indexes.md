---
title: "Criar e gerenciar &#237;ndices de texto completo | Microsoft Docs"
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
  - "índices de texto completo [SQL Server], sobre"
ms.assetid: f8a98486-5438-44a8-b454-9e6ecbc74f83
caps.latest.revision: 23
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 20
---
# Criar e gerenciar &#237;ndices de texto completo
  As informações contidas em índices de texto completo são usadas pelo Mecanismo de Texto Completo para compilar consultas de texto completo que podem procurar determinadas palavras ou combinações de palavras rapidamente em uma tabela. Um índice de texto completo armazena informações sobre palavras importantes e sua localização em uma ou mais colunas de uma tabela de banco de dados. Um índice de texto completo consiste em um tipo especial de índice funcional com base em token que é criado e mantido pelo Mecanismo de Texto Completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O processo de criação de um índice de texto completo é diferente da criação de outros tipos de índices. Em vez de criar uma estrutura de árvore B com base em um valor armazenado em uma linha específica, o Mecanismo de Texto Completo cria uma estrutura de índice compactada, empilhada e invertida com base em tokens individuais do texto que está sendo indexado.  O tamanho de um índice de texto completo é limitado apenas pelos recursos de memória disponíveis do computador no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada.  
  
 A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], os índices de texto completo são integrados ao Mecanismo de Banco de Dados e deixam de residir no sistema de arquivos, como ocorria nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Em um novo banco de dados, agora o catálogo de texto completo é um objeto virtual que não pertence a nenhum grupo de arquivos; ele é simplesmente um conceito lógico que faz referência a um grupo dos índices de texto completo. Porém, observe que, durante a atualização de um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], para qualquer catálogo de texto completo que contenha arquivos de dados, é criado um novo grupo de arquivos. Para obter mais informações, veja [Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  
> [!NOTE]  
>  No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores, o Mecanismo de Texto Completo reside no processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e não em um serviço separado. A integração do Mecanismo de Texto Completo ao Mecanismo de Banco de Dados melhora a capacidade de gerenciamento de texto completo, a otimização de consultas mistas e o desempenho como um todo.  
  
 Só é permitido um índice de texto completo por tabela. Para que um índice de texto completo seja criado em uma tabela, a tabela deve ter uma única coluna não nula exclusiva. É possível criar um índice de texto completo em colunas do tipo **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary** e **varbinary(max)**, que podem ser indexadas para a pesquisa de texto completo. A criação de um índice de texto completo em uma coluna cujo tipo de dados é **varbinary**, **varbinary(max)**, **image** ou **xml** exige a especificação de uma coluna de tipo. Uma *coluna de tipo* consiste em uma coluna de tabela em que você armazena a extensão de arquivo (.doc, .pdf, .xls, etc.) do documento em cada linha.  
  
 O processo de criar e manter um índice de texto completo é chamado de *população* (também conhecido como *rastreamento*). Existem três tipos de população de índice de texto completo: população completa, população com base em controle de alterações e população incremental com base em carimbo de data e hora. Para obter mais informações, veja [Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  
##  <a name="tasks"></a> Tarefas comuns  
 **Para criar um índice de texto completo**  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)  
  
 **Para alterar um índice de texto completo**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
 **Para descartar um índice de texto completo**  
  
-   [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)  
  
 [Neste tópico](#top)  
  
##  <a name="structure"></a> Estrutura de índice de texto completo  
 Um bom conhecimento da estrutura do índice de texto completo ajudará você a entender como funciona o Mecanismo de Texto Completo. Este tópico usa o trecho a seguir da tabela **Document** em [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] como tabela de exemplo. Esse trecho mostra apenas duas colunas, **DocumentID** e **Title**, e três linhas da tabela.  
  
 Para este exemplo, assumiremos que um índice de texto completo foi criado na coluna **Title**.  
  
|DocumentID|Título|  
|----------------|-----------|  
|1|Crank Arm and Tire Maintenance|  
|2|Front Reflector Bracket and Reflector Assembly 3|  
|3|Front Reflector Bracket Installation|  
  
 Por exemplo, a tabela a seguir, que mostra o Fragment 1, descreve o conteúdo do índice de texto completo criado na coluna **Title** da tabela **Document**. Os índices de texto completo contêm mais informações do que é apresentado nessa tabela. A tabela é uma representação lógica de um índice de texto completo e é fornecida somente para fins de demonstração. As linhas são armazenadas em um formato compactado para otimizar o uso do disco.  
  
 Observe que os dados foram invertidos em relação aos documentos originais. A inversão ocorre porque as palavras-chave são mapeadas para as IDs de documento. Por esse motivo, geralmente um índice de texto completo é chamado de índice invertido.  
  
 Observe também que a palavra-chave "and" foi removida do índice de texto completo. Isso ocorre porque "and" é uma palavra irrelevante e remover essas palavras de um índice de texto completo pode levar a economias consideráveis do espaço em disco, melhorando o desempenho de consulta. Para obter mais informações sobre palavras irrelevantes, veja [Configurar e gerenciar palavras irrelevantes (stop words) e listas de palavras irrelevantes para pesquisa de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
 **Fragmento 1**  
  
|Palavra-chave|ColId|DocId|Ocorrência|  
|-------------|-----------|-----------|----------------|  
|Crank|1|1|1|  
|Arm|1|1|2|  
|Tire|1|1|4|  
|Manutenção|1|1|5|  
|Front|1|2|1|  
|Front|1|3|1|  
|Reflector|1|2|2|  
|Reflector|1|2|5|  
|Reflector|1|3|2|  
|Bracket|1|2|3|  
|Bracket|1|3|3|  
|Assembly|1|2|6|  
|3|1|2|7|  
|Instalação|1|3|4|  
  
 A coluna **Keyword** contém uma representação de um único token extraído no momento da indexação. Os separadores de palavras determinam o que compõe um token.  
  
 A coluna **ColId** contém um valor que corresponde a uma coluna específica indexada com texto completo.  
  
 A coluna **DocId** contém valores para um inteiro de oito bytes que é mapeado para um valor de chave de texto completo específico em uma tabela indexada com texto completo. Esse mapeamento é necessário quando a chave de texto completo não é um tipo de dados integer. Em casos como esses, os mapeamentos entre valores de chave de texto completo e valores da coluna **DocId** são mantidos em uma tabela à parte, chamada tabela de Mapeamento de DocId. Para examinar esses mapeamentos, use o procedimento armazenado do sistema [sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md). Para atender a um critério de pesquisa, os valores de DocId da tabela acima precisam ser unidos à tabela de mapeamento DocId para recuperar linhas da tabela base que está sendo consultada. Se o valor da chave de texto completo da tabela base for do tipo inteiro, o valor funcionará diretamente como DocId, e nenhum mapeamento será necessário. Por isso, o uso de valores de chave de texto completo pode ajudar a otimizar consultas de texto completo.  
  
 A coluna **Occurrence** contém um valor inteiro. Para cada valor de DocId, há uma lista de valores de ocorrência que correspondem aos deslocamentos relativos de palavras de uma palavra-chave específica dentro de DocId. Os valores de ocorrência são úteis para definir as correspondências de frase ou de proximidade, por exemplo, as frases têm valores de ocorrência numericamente adjacentes. Eles também são úteis para calcular pontuações de relevância; por exemplo, o número de ocorrências de uma palavra-chave em DocId pode ser usado na pontuação.  
  
 [Neste tópico](#top)  
  
##  <a name="fragments"></a> Fragmentos de índice de texto completo  
 O índice de texto completo lógico normalmente é dividido entre várias tabelas internas. Cada tabela interna é chamada de fragmento de índice de texto completo. Alguns desses fragmentos podem conter dados mais novos do que outros. Por exemplo, se um usuário atualiza a linha a seguir cujo DocId é 3 e a tabela tem controle de alterações automático, é criado um novo fragmento.  
  
|DocumentID|Título|  
|----------------|-----------|  
|3|Refletor traseiro|  
  
 No exemplo a seguir, que mostra o Fragmento 2, o fragmento contém dados mais recentes sobre DocId 3 em comparação com Fragmento 1. Portanto, quando o usuário procura por “Refletor Traseiro", os dados de Fragmento 2 são usados para DocId 3. Cada fragmento é marcado com um carimbo de data/hora da criação, que pode ser consultado usando a exibição de catálogo [sys.fulltext_index_fragments](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md).  
  
 **Fragmento 2**  
  
|Palavra-chave|ColId|DocId|Occ|  
|-------------|-----------|-----------|---------|  
|Traseiro|1|3|1|  
|Reflector|1|3|2|  
  
 Como pode ser visto no Fragmento 2, as consultas de texto completo precisam examinar cada fragmento internamente e descartar entradas mais antigas. Por isso, um número excessivo de fragmentos de índice de texto completo no índice de texto completo pode levar a uma diminuição considerável do desempenho de consulta. Para reduzir o número de fragmentos, reorganize o catálogo de texto completo usando a opção REORGANIZE da instrução [ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)]. Essa instrução executa uma *mesclagem mestra* que mescla os fragmentos em um único fragmento maior e remove todas as entradas obsoletas do índice de texto completo.  
  
 Depois de reorganizado, o índice de exemplo conterá as linhas seguintes:  
  
|Palavra-chave|ColId|DocId|Occ|  
|-------------|-----------|-----------|---------|  
|Crank|1|1|1|  
|Arm|1|1|2|  
|Tire|1|1|4|  
|Manutenção|1|1|5|  
|Front|1|2|1|  
|Traseiro|1|3|1|  
|Reflector|1|2|2|  
|Reflector|1|2|5|  
|Reflector|1|3|2|  
|Bracket|1|2|3|  
|Assembly|1|2|6|  
|3|1|2|7|  
  
 [Neste tópico](#top)  
  
  