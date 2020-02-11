---
title: SQLFetchScroll (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetchScroll function [ODBC], Cursor Library
ms.assetid: 4417e57c-31dd-475e-8fe9-eab00a459c80
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16e7e4d133fdfafd7a005c19b0a2943b2ea9ef6d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086450"
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLFetchScroll** na biblioteca de cursores. Para obter informações gerais sobre **SQLFetchScroll**, consulte [SQLFetchScroll function](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
 A biblioteca de cursores implementa o **SQLFetchScroll** chamando **SQLFetch** repetidamente no driver. Ele transfere os dados recuperados do driver para os buffers de conjunto de linhas fornecidos pelo aplicativo. Ele também armazena em cache os dados na memória e nos arquivos de disco. Quando um aplicativo solicita um novo conjunto de linhas, a biblioteca de cursores recupera-o conforme necessário do driver (se ele não tiver sido previamente buscado) ou o cache (se tiver sido previamente buscado). Por fim, a biblioteca de cursores mantém o status dos dados armazenados em cache e retorna essas informações para o aplicativo na matriz de status de linha.  
  
 Quando a biblioteca de cursores é usada, as chamadas para **SQLFetchScroll** não podem ser misturadas com chamadas para **SQLFetch** ou **SQLExtendedFetch**.  
  
 Quando a biblioteca de cursores é usada, as chamadas para **SQLFetchScroll** têm suporte para ODBC 2. *x* e para ODBC 3. drivers *x* .  
  
## <a name="rowset-buffers"></a>Buffers de conjunto de linhas  
 A biblioteca de cursores otimiza a transferência de dados do driver para o buffer do conjunto de linhas fornecido pelo aplicativo se:  
  
-   O aplicativo usa a associação de linha.  
  
-   Não há nenhum byte não utilizado entre os campos na estrutura que o aplicativo declara para manter uma linha de dados.  
  
-   Os campos nos quais **SQLFetch** ou **SQLFetchScroll** retorna o comprimento/indicador de uma coluna segue o buffer para essa coluna e precede o buffer para a próxima coluna. Esses campos são opcionais.  
  
 Quando o aplicativo solicita um novo conjunto de linhas, a biblioteca de cursores recupera dados de seu cache e do driver, conforme necessário. Se os conjuntos de linhas novos e antigos se sobrepõem, a biblioteca de cursores pode otimizar seu desempenho reutilizando os dados das seções sobrepostas dos buffers de conjunto de linhas. Portanto, as alterações não salvas nos buffers de conjunto de linhas são perdidas, a menos que os conjuntos de itens novos e antigos se sobreponham e as alterações estejam nas seções sobrepostas dos buffers de conjunto de linhas. Para salvar as alterações, um aplicativo envia uma instrução UPDATE posicionada.  
  
 Observe que a biblioteca de cursores sempre atualiza os buffers de conjunto de linhas com dados do cache quando um aplicativo chama **SQLFetchScroll** com o argumento *FetchOrientation* definido como SQL_FETCH_RELATIVE e o argumento *FetchOffset* definido como 0.  
  
 A biblioteca de cursores dá suporte à chamada de **SQLSetStmtAttr** com um *atributo* de SQL_ATTR_ROW_ARRAY_SIZE para alterar o tamanho do conjunto de linhas enquanto um cursor está aberto. O novo tamanho do conjunto de linhas entrará em vigor na próxima vez que **SQLFetchScroll** for chamado.  
  
## <a name="result-set-membership"></a>Associação do conjunto de resultados  
 A biblioteca de cursores recupera dados do driver somente quando o aplicativo o solicita. Dependendo da fonte de dados e da configuração do atributo da instrução SQL_CONCURRENCY, isso tem as seguintes consequências:  
  
-   Os dados recuperados pela biblioteca de cursores podem diferir dos dados que estavam disponíveis no momento em que a instrução foi executada. Por exemplo, depois que o cursor foi aberto, as linhas inseridas em um ponto além da posição atual do cursor podem ser recuperadas por alguns drivers.  
  
-   Os dados no conjunto de resultados podem ser bloqueados pela fonte de dados para a biblioteca de cursores e, portanto, não estarão disponíveis para outros usuários.  
  
 Depois que a biblioteca de cursores armazenou em cache uma linha de dados, ela não pode detectar alterações nessa linha na fonte de dados subjacente (exceto atualizações e exclusões posicionadas no cache do mesmo cursor). Isso ocorre porque, para chamadas para **SQLFetchScroll**, a biblioteca de cursores nunca recupera os dados da fonte de dados. Em vez disso, ele recupera dados de seu cache.  
  
## <a name="scrolling"></a>Rolagem  
 A biblioteca de cursores dá suporte aos seguintes tipos de busca no **SQLFetchScroll**.  
  
|Tipo de cursor|Tipos de busca|  
|-----------------|-----------------|  
|Somente avanço|SQL_FETCH_NEXT|  
|Estático|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>Errors  
 Quando **SQLFetchScroll** é chamado e uma das chamadas para **sqlfetch** retorna SQL_ERROR, a biblioteca de cursores prossegue da seguinte maneira. Depois de concluir essas etapas, a biblioteca de cursores continuará processando.  
  
1.  Chama **SQLGetDiagRec** para obter informações de erro do driver e posta isso como um registro de diagnóstico no Gerenciador de driver.  
  
2.  Define o campo SQL_DIAG_ROW_NUMBER no registro de diagnóstico para o valor apropriado.  
  
3.  Define o campo SQL_DIAG_COLUMN_NUMBER no registro de diagnóstico para o valor apropriado, se aplicável; caso contrário, ele o definirá como 0.  
  
4.  Define o valor da linha em erro na matriz de status de linha para SQL_ROW_ERROR.  
  
 Depois que a biblioteca de cursores chamou **SQLFetch** várias vezes em sua implementação de **SQLFetchScroll**, qualquer erro ou aviso retornado por uma das chamadas para **SQLFetch** estará em um registro de diagnóstico e poderá ser recuperado por uma chamada para **SQLGetDiagRec**. Se os dados foram truncados quando foram buscados, os dados truncados agora residem no cache da biblioteca de cursores. As chamadas subsequentes para **SQLFetchScroll** para rolar para uma linha com dados truncados retornarão os dados truncados e nenhum aviso será gerado porque os dados são buscados no cache da biblioteca de cursores. Para controlar o comprimento dos dados retornados para que ele possa determinar se os dados retornados em um buffer foram truncados, um aplicativo deve ligar o buffer de comprimento/indicador.  
  
## <a name="bookmark-operations"></a>Operações de indicador  
 A biblioteca de cursores dá suporte à chamada de **SQLFetchScroll** com um *FetchOrientation* de SQL_FETCH_BOOKMARK. Ele também dá suporte à especificação de um deslocamento no argumento *FetchOffset* que pode ser usado na operação de indicador. Essa é a única operação de indicador à qual a biblioteca de cursores dá suporte. A biblioteca de cursores não dá suporte à chamada de **SQLBulkOperations**.  
  
 Se o aplicativo tiver definido o atributo SQL_ATTR_USE_BOOKMARKS Statement e tiver associado à coluna Bookmark, a biblioteca de cursores gerará um indicador de comprimento fixo e o retornará ao aplicativo. A biblioteca de cursores cria e mantém os indicadores que ele usa; Ele não usa indicadores mantidos na fonte de dados. Quando **SQLFetchScroll** é chamado para recuperar um bloco de dados que já foi buscado da fonte de dados, ele recupera os dados do cache da biblioteca de cursores. Como resultado, o indicador usado em uma chamada para **SQLFetchScroll** com um *FetchOrientation* de SQL_FETCH_BOOKMARK deve ser criado e mantido pela biblioteca de cursores.  
  
## <a name="interaction-with-other-functions"></a>Interação com outras funções  
 Um aplicativo deve chamar **SQLFetch** ou **SQLFetchScroll** antes de preparar ou executar quaisquer instruções UPDATE ou DELETE posicionadas.
