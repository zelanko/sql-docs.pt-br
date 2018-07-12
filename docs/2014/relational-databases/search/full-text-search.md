---
title: Pesquisa de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server]
ms.assetid: a0ce315d-f96d-4e5d-b4eb-ff76811cab75
caps.latest.revision: 47
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5b923b9b27fd7b67d61b25956f3d44102f1a5f79
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37158017"
---
# <a name="full-text-search"></a>Pesquisa de Texto Completo
  A Pesquisa de Texto Completo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] permite que usuários e aplicativos executem consultas de texto completo em dados baseados em caracteres nas tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para que você possa executar consultas de texto completo em uma tabela, o administrador de banco de dados deve criar um índice de texto completo na tabela. O índice de texto completo inclui uma ou mais colunas baseadas em caractere da tabela. Essas colunas podem ter qualquer um dos seguintes tipos de dados: `char`, `varchar`, `nchar`, `nvarchar`, `text`, `ntext`, `image`, `xml`, ou `varbinary(max)` e FILESTREAM. Cada índice de texto completo indexa uma ou mais colunas da tabela base, e cada coluna pode usar um idioma específico.  
  
 As consultas de texto completo executam pesquisas linguísticas nos dados de texto em índices de texto completo trabalhando em palavras e frases com base em regras de um idioma específico, como inglês ou japonês. As consultas de texto completo podem incluir palavras e frases simples ou várias formas de uma palavra ou frase. Uma consulta de texto completo retorna todos os documentos que contiverem, pelo menos, uma correspondência (também conhecida como uma *ocorrência*). Uma correspondência ocorre quando um documento de destino contém todos os termos especificados na consulta de texto completo e atende a quaisquer outros critérios de pesquisa, como a distância entre os termos correspondentes.  
  
> [!NOTE]  
>  Pesquisa de texto completo é um componente opcional do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados. Para obter mais informações, consulte [instalar o SQL Server 2014](../../database-engine/install-windows/install-sql-server.md).  
  
##  <a name="benefits"></a> O que pode fazer com a pesquisa de texto completo?  
 A pesquisa de texto completo é aplicável a uma grande variedade de cenários comerciais, como e-business, para procurar por itens em um site; escritórios de advocacia, para procurar por históricos de casos em um repositório de dados legais; ou departamentos de RH, para comparar descrições de vagas de trabalho a currículos armazenados. As tarefas básicas de administração e desenvolvimento da pesquisa de texto completo são equivalentes, independentemente dos cenários comerciais. No entanto, em um dado cenário comercial, as consultas e o índice de texto completo podem ser ajustados para atender a metas comerciais. Por exemplo, em um cenário de e-business, maximizar o desempenho deve ser mais importante do que a classificação de resultados, a precisão da recuperação (quantas correspondências existentes são de fato retornadas por uma consulta de texto completo) ou o suporte a vários idiomas. Em um escritório de advocacia, retornar cada acerto possível (*recuperação total* de informações) deve ser o aspecto mais importante a ser considerado.  
  
 [Neste tópico](#top)  
  
###  <a name="queries"></a> Consultas de pesquisa de texto completo  
 Depois que colunas forem adicionadas a um índice de texto completo, os usuários e aplicativos poderão executar consultas de texto completo no texto das colunas. Essas consultas podem procurar qualquer um dos seguintes itens:  
  
-   Uma ou mais palavras ou frases específicas (*termo simples*)  
  
-   Uma palavra ou frase na qual as palavras começam com o texto especificado (*termo de prefixo*)  
  
-   As formas flexionadas de uma palavra específica (*termo de geração*)  
  
-   Uma palavra ou frase perto de outra palavra ou frase (*termo de proximidade*).  
  
-   Os sinônimos de uma palavra específica (*dicionário de sinônimos*)  
  
-   Palavras ou frases que usam valores ponderados (*termo ponderado*)  
  
 As consultas de texto completo não diferenciam maiúsculas de minúsculas. Por exemplo, a pesquisa de "Alumínio" ou "alumínio" retorna os mesmos resultados.  
  
 As consultas de texto completo usam um pequeno conjunto de predicados [!INCLUDE[tsql](../../../includes/tsql-md.md)] (CONTAINS e FREETEXT) e funções (CONTAINSTABLE e FREETEXTTABLE). Entretanto, as metas de pesquisa de um determinado cenário comercial influenciam a estrutura das consultas de texto completo. Por exemplo:  
  
-   E-business — procurar por um produto em um site:  
  
    ```  
    SELECT product_id   
    FROM products   
    WHERE CONTAINS(product_description, "Snap Happy 100EZ"  
        OR FORMSOF(THESAURUS,'Snap Happy')  
        OR '100EZ')   
    AND product_cost < 200 ;  
    ```  
  
-   Cenário de recrutamento — procurar candidatos a uma vaga de trabalho que tenham experiência prática com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
    ```  
    SELECT candidate_name,SSN   
    FROM candidates   
    WHERE CONTAINS(candidate_resume,"SQL Server") AND candidate_division = 'DBA';  
    ```  
  
 Para obter mais informações, veja [Consulta com pesquisa de texto completo](query-with-full-text-search.md).  
  
 [Neste tópico](#top)  
  
###  <a name="like"></a> Comparando LIKE à pesquisa de texto completo  
 Ao contrário da pesquisa de texto completo, o predicado [LIKE](/sql/t-sql/language-elements/like-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] funciona apenas em padrões de caracteres. Além disso, não é possível usar o predicado LIKE para consultar dados binários formatados. Além disso, uma consulta LIKE feita em uma grande quantidade de dados de texto não estruturados é bem mais lenta do que uma consulta de texto completo equivalente feita nos mesmos dados. Uma consulta LIKE executada em milhões de linhas de dados de texto pode demorar muitos minutos, enquanto uma consulta de texto completo pode demorar alguns segundos ou menos para ser executada nos mesmos dados, dependendo do número de linhas retornadas.  
  
 [Neste tópico](#top)  
  
##  <a name="architecture"></a> Componentes e arquitetura de pesquisa de texto completo  
 A arquitetura de pesquisa de texto completo é formada pelos seguintes processos:  
  
-   O processo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (sqlservr.exe).  
  
-   O processo de host do daemon de filtro (fdhost.exe).  
  
     Por motivos de segurança, os filtros são carregados por processos separados que são chamados de hosts do daemon de filtro. Os processos fdhost.exe são criados por um serviço Iniciador FDHOST (MSSQLFDLauncher) e executados sob as credenciais de segurança da conta deste serviço. Por isso, o serviço Iniciador FDHOST deve estar em execução para que a indexação de texto completo e a consulta de texto completo funcionem. Para obter informações sobre como configurar a conta de serviço para esse serviço, veja [Definir a conta de serviço do Iniciador do Daemon de Filtro de Texto Completo](set-the-service-account-for-the-full-text-filter-daemon-launcher.md).  
  
 Esses dois processos contêm os componentes da arquitetura de pesquisa de texto completo. Esses componentes e suas relações são resumidas na ilustração a seguir. Os componentes são descritos após a ilustração.  
  
 ![Arquitetura de pesquisa de texto completo](../../database-engine/media/ifts-arch.gif "Arquitetura de pesquisa de texto completo")  
  
 [Neste tópico](#top)  
  
###  <a name="sqlprocess"></a> Processo do SQL Server  
 O processo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa os seguintes componentes na pesquisa de texto completo:  
  
-   **Tabelas de usuário.** Essas tabelas contêm os dados para serem indexados com texto completo.  
  
-   **Gatherer de texto completo.** O gatherer de texto completo funciona com os threads de rastreamento de texto completo. Ele é responsável por agendar e orientar a população de índices de texto completo e também por monitorar os catálogos de texto completo.  
  
-   **Arquivos de dicionário de sinônimos.** Esses arquivos contêm sinônimos de termos de pesquisa. Para obter mais informações, veja [Configurar e gerenciar arquivos de dicionário de sinônimos para pesquisa de texto completo](configure-and-manage-thesaurus-files-for-full-text-search.md).  
  
-   **Objetos da lista de palavras irrelevantes (stoplist).** Os objetos da lista de palavras irrelevantes contêm uma lista de palavras comuns que não são úteis para a pesquisa. Para obter mais informações, veja [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
-   **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] processador de consultas.** O processador de consulta compila e executa consultas SQL. Se uma consulta SQL incluir uma consulta de pesquisa de texto completo, a consulta será enviada ao Mecanismo de Texto Completo, durante a compilação e durante a execução. O resultado da consulta é comparado com o índice de texto completo.  
  
-   **Mecanismo de Texto Completo.** O Mecanismo de Texto Completo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está totalmente integrado ao processador de consultas. O Mecanismo de Texto Completo compila e executa consultas de texto completo. Como parte da execução da consulta, o Mecanismo de Texto Completo pode receber entrada do dicionário de sinônimos e da lista de palavras irrelevantes.  
  
-   **Gravador de índice (indexador).** O gravador de índice cria a estrutura usada para armazenar os tokens indexados.  
  
-   **Gerenciador de daemon de filtro.** O gerenciador de daemon de filtro é responsável por monitorar o status do host do daemon de filtro do Mecanismo de Texto Completo.  
  
 [Neste tópico](#top)  
  
###  <a name="fdhostprocess"></a> Processo de Host do Daemon de filtro  
 O host do daemon de filtro é um processo que é iniciado pelo Mecanismo de Texto Completo. Ele executa os seguintes componentes de pesquisa de texto completo que são responsáveis por acessar, filtrar e separar palavras de dados de tabelas, bem como por separar palavras e lematizar a entrada da consulta.  
  
 Os componentes do host do daemon de filtro são os seguintes:  
  
-   **Manipulador de protocolo.** Esse componente extrai os dados da memória para processamento adicional e acessa dados de uma tabela de usuário de um banco de dados especificado. Uma de suas responsabilidades é coletar dados das colunas que estão sendo indexadas com texto completo e transmiti-los ao host do daemon de filtro, que aplicará a filtragem e o separador de palavras conforme exigido.  
  
-   **Filtros.** Alguns tipos de dados requerem filtragem para que os dados contidos em um documento possam ser indexados com texto completo, inclusive dados em colunas `varbinary`, `varbinary(max)`, `image` ou `xml`. O filtro usado para um dado documento depende de seu tipo de documento. Por exemplo, são usados filtros diferentes para documentos do Microsoft Word (.doc), do Microsoft Excel (.xls) e no formato XML (.xml). O filtro extrai partes de texto do documento, removendo a formatação inserida e mantendo o texto e, potencialmente, as informações sobre a posição deste. O resultado é um fluxo de informações textuais. Para obter mais informações, veja [Configurar e gerenciar filtros para pesquisa](configure-and-manage-filters-for-search.md).  
  
-   **Separadores de palavras e lematizadores.** Um separador de palavras é um componente específico a um idioma que encontra limites de palavras com base nas regras lexicais de determinado idioma (*separação de palavras*). Cada separador de palavras é associado a um componente lematizador específico do idioma, que conjuga verbos e executa expansões flexionadas. No momento da indexação, o host do daemon de filtro usa um separador de palavras e um lematizador para executar a análise linguística dos dados textuais de uma determinada coluna de tabela. O idioma associado a uma coluna de tabela no índice de texto completo determina qual separador de palavras e qual lematizador são usados para indexar a coluna. Para obter mais informações, veja [Configurar e gerenciar separadores de palavras e lematizadores para pesquisa](configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
 [Neste tópico](#top)  
  
##  <a name="processing"></a> Processamento da pesquisa de texto completo  
 A pesquisa de texto completo é ativada pelo Mecanismo de Texto Completo. O Mecanismo de Texto Completo tem duas funções: suporte a indexação e suporte a consulta.  
  
###  <a name="indexing"></a> Processo de indexação de texto completo  
 Quando uma população de texto completo (também conhecida como rastreamento) é iniciada, o mecanismo de texto completo entrega grandes lotes de dados à memória e notifica o host do daemon de filtro. O host filtra e o Word divide os dados e converte os dados convertidos em listas de palavras invertidas. A pesquisa de texto completo pega os dados convertidos nas listas de palavras, processa-os para remover palavras irrelevantes e mantém as listas de palavras para um lote em um ou mais índices invertidos.  
  
 Ao indexar dados armazenados em um `varbinary(max)` ou `image` coluna, o filtro, que implementa o **IFilter** interface, extrai texto com base no formato de arquivo especificado para os dados (por exemplo, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word). Em alguns casos, os componentes de filtro exigem o `varbinary(max)`, ou `image` dados sejam gravados fora da pasta, em vez de serem postos na memória.  
  
 Como parte do processamento, os dados de texto reunidos são passados por um separador de palavras para que o texto seja separado em tokens individuais ou palavras-chave. A linguagem usada para geração de tokens é especificada no nível da coluna, podendo ser identificada em dados `varbinary(max)`, `image` ou `xml`, pelo componente de filtro.  
  
 Processamentos adicionais podem ser realizados para remover palavras irrelevantes e para normalizar os tokens antes de eles serem armazenados no índice de texto completo ou em um fragmento de índice.  
  
 Quando a população for concluída, um processo de mesclagem final será disparado, mesclando os fragmentos de índice em um índice de texto completo mestre. Isso resulta em desempenho aprimorado de consultas, uma vez que apenas o índice precisa ser consultado, em vez de uma série de fragmentos de índice, e melhores estatísticas de pontuação podem ser usadas para classificação de relevância.  
  
 [Neste tópico](#top)  
  
###  <a name="querying"></a> Processo de consulta de texto completo  
 O processador de consultas passa as partes do texto completo de uma consulta para o Mecanismo de Texto Completo para processamento. O Mecanismo de Texto Completo executa a quebra de palavras e, opcionalmente, expansões do dicionário de sinônimos, lematização e processamento de palavras irrelevantes (palavras de ruído). Em seguida, as partes de texto completo da consulta são representadas na forma de operadores SQL, principalmente como STVFs (funções com valor de tabela de fluxo). Durante a execução da consulta, essas STVFs acessam o índice invertido para recuperar os resultados corretos. Os resultados são retornados para o cliente neste momento ou processados mais um pouco antes de serem retornados ao cliente.  
  
 [Neste tópico](#top)  
  
##  <a name="components"></a> Componentes linguísticos e suporte de idioma na pesquisa de texto completo  
 A pesquisa de texto completo oferece suporte a quase 50 idiomas diferentes, como inglês, espanhol, chinês, japonês, árabe, bengalês e híndi. Para obter uma lista completa dos idiomas de texto completo com suporte, veja [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql). Cada uma das colunas do índice de texto completo é associada a um LCID (identificador de localidade) do Microsoft Windows que equivale a um idioma suportado pela pesquisa de texto completo. Por exemplo, o LCID 1033 equivale ao inglês norte-americano e o LCID 2057, ao inglês britânico. Para cada idioma de texto completo suportado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece componentes linguísticos que dão suporte à indexação e à consulta de dados de texto completo armazenados nesse idioma.  
  
 Os componentes específicos de idioma incluem:  
  
-   **Separadores de palavras e lematizadores.** Um separador de palavras encontra limites de palavras com base nas regras lexicais de determinado idioma (*separação de palavras*). Cada separador de palavras é associado a um lematizador que conjuga verbos desse idioma. Para obter mais informações, veja [Configurar e gerenciar separadores de palavras e lematizadores para pesquisa](configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
-   **Listas de palavras irrelevantes.** É fornecida uma lista de palavras irrelevantes (stoplist) do sistema, que contém um conjunto básico de palavras irrelevantes (também chamadas de palavras de ruído). Uma *palavra irrelevante* consiste em uma palavra que não ajuda a pesquisa e é ignorada por consultas de texto completo. Por exemplo, no português, palavras como "um/uma", "e", "é" e "o/a" são consideradas palavras irrelevantes. Normalmente, é preciso configurar um ou mais arquivos de dicionário de sinônimos e listas de palavras irrelevantes. Para obter mais informações, veja [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
-   **Arquivos de dicionário de sinônimos.** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] também instala um arquivo de dicionário de sinônimos para cada idioma de texto completo, bem como um arquivo de dicionário de sinônimos global. Os arquivos de dicionário de sinônimos instalados são basicamente vazios, mas você pode editá-los para definir sinônimos para um determinado cenário comercial ou de idioma. Ao desenvolver um dicionário de sinônimos personalizado para seus dados de texto completo, você pode efetivamente ampliar o escopo de consultas de texto completo baseadas nesses dados. Para obter mais informações, veja [Configurar e gerenciar arquivos de dicionário de sinônimos para pesquisa de texto completo](configure-and-manage-thesaurus-files-for-full-text-search.md).  
  
-   **Filtros (iFilters).**  A indexação de um documento em uma coluna de tipo de dados `varbinary(max)`, `image` ou `xml` requer um filtro para executar processamento extra. O filtro deve ser específico do tipo de documento (.doc, .pdf, .xls, .xml e assim por diante). Para obter mais informações, veja [Configurar e gerenciar filtros para pesquisa](configure-and-manage-filters-for-search.md).  
  
 Os separadores de palavras (e lematizadores) e filtros são executados no processo do host do daemon de filtro (fdhost.exe).  
  
 [Neste tópico](#top)  
  
##  <a name="reltasks"></a> Tarefas relacionadas  
  
-   [Iniciar a pesquisa de texto completo](get-started-with-full-text-search.md)  
  
-   Escrevendo consultas de texto completo  
  
    -   [Consulta com pesquisa de texto completo](query-with-full-text-search.md)  
  
    -   [Pesquisar palavras próximas de outra palavra com NEAR](search-for-words-close-to-another-word-with-near.md)  
  
    -   [Limitar resultados da pesquisa com RANK](limit-search-results-with-rank.md)  
  
    -   [Melhorar o desempenho de consultas de texto completo](improve-the-performance-of-full-text-queries.md)  
  
    -   [Pesquisar propriedades de documento com listas de propriedades de pesquisa](search-document-properties-with-search-property-lists.md)  
  
    -   [Localizar GUIDs do conjunto de propriedades e IDs de inteiro de propriedade para propriedades de pesquisa](find-property-set-guids-and-property-integer-ids-for-search-properties.md)  
  
-   Gerenciando catálogos e índices  
  
    -   [Criar e gerenciar catálogos de texto completo](create-and-manage-full-text-catalogs.md)  
  
    -   [Criar e gerenciar índices de texto completo](create-and-manage-full-text-indexes.md)  
  
    -   [Escolher um idioma ao criar um índice de texto completo](choose-a-language-when-creating-a-full-text-index.md)  
  
    -   [Popular índices de texto completo](populate-full-text-indexes.md)  
  
    -   [Administrar índices de texto completo](../../database-engine/manage-full-text-indexes.md)  
  
    -   [Melhorar o desempenho de índices de texto completo](improve-the-performance-of-full-text-indexes.md)  
  
    -   [Solucionar problemas na indexação de texto completo](troubleshoot-full-text-indexing.md)  
  
    -   [Fazer backup e restaurar índices e catálogos de texto completo](back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
-   Gerenciando os componentes linguísticos  
  
    -   [Configurar e gerenciar filtros de pesquisa](configure-and-manage-filters-for-search.md)  
  
    -   [Configurar e gerenciar separadores de palavras e lematizadores de pesquisa](configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
    -   [Exibir ou alterar filtros registrados e separadores de palavras](view-or-change-registered-filters-and-word-breakers.md)  
  
    -   [Reverter à versão anterior os separadores de palavras usados pela pesquisa](revert-the-word-breakers-used-by-search-to-the-previous-version.md)  
  
    -   [Alterar o separador de palavras usado para inglês dos EUA e inglês do Reino Unido](change-the-word-breaker-used-for-us-english-and-uk-english.md)  
  
    -   [Personalizar o comportamento de separadores de palavras com um dicionário personalizado](customize-the-behavior-of-word-breakers-with-a-custom-dictionary.md)  
  
    -   [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
    -   [Configurar e gerenciar arquivos de dicionário de sinônimos para pesquisa de texto completo](configure-and-manage-thesaurus-files-for-full-text-search.md)  
  
-   Gerenciando a pesquisa de texto completo  
  
    -   [Gerenciar e monitorar a pesquisa de texto completo em uma instância do servidor](manage-and-monitor-full-text-search-for-a-server-instance.md)  
  
    -   [Definir a conta de serviço do Iniciador do Daemon de Filtro de Texto Completo](set-the-service-account-for-the-full-text-filter-daemon-launcher.md)  
  
-   [Atualizar pesquisa de texto completo](upgrade-full-text-search.md)  
  
 [Neste tópico](#top)  
  
##  <a name="relcontent"></a> Conteúdo relacionado  
  
-   [DDL, funções, procedimentos armazenados e exibições de pesquisa de texto completo](../views/views.md)  
  
 [Neste tópico](#top)  
  
  
