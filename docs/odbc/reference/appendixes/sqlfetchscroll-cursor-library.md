---
title: SQLFetchScroll (biblioteca de Cursor) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLFetchScroll function [ODBC], Cursor Library
ms.assetid: 4417e57c-31dd-475e-8fe9-eab00a459c80
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 85647e81245e8e5e76e79cd285bc73b8ff6fb364
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll (biblioteca de Cursor)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLFetchScroll** função na biblioteca de cursor. Para obter informações gerais sobre **SQLFetchScroll**, consulte [função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
 A biblioteca de cursores implementa **SQLFetchScroll** chamando repetidamente **SQLFetch** no driver. Ele transfere os dados recuperados do driver aos buffers de linhas fornecidos pelo aplicativo. Ele também armazena em cache os dados em arquivos de disco e memória. Quando um aplicativo solicita um novo conjunto de linhas, a biblioteca de cursores recupera-lo conforme necessário de driver (se ele não foi previamente buscado) ou cache (se ele foi buscado anteriormente). Finalmente, a biblioteca de cursores mantém o status dos dados armazenados em cache e retorna essas informações para o aplicativo na matriz de status de linha.  
  
 Quando a biblioteca de cursores é usada, chamadas para **SQLFetchScroll** não podem ser misturadas a chamadas para o **SQLFetch** ou **SQLExtendedFetch**.  
  
 Quando a biblioteca de cursores é usada, chamadas para **SQLFetchScroll** são com suporte tanto para o ODBC 2. *x* e para o ODBC 3. *x* drivers.  
  
## <a name="rowset-buffers"></a>Buffers de conjunto de linhas  
 A biblioteca de cursores otimiza a transferência de dados do driver para o buffer de linhas fornecido pelo aplicativo se:  
  
-   O aplicativo usa a associação.  
  
-   Não há nenhum bytes não utilizados entre campos na estrutura de que aplicativo declara para manter uma linha de dados.  
  
-   Os campos nos quais **SQLFetch** ou **SQLFetchScroll** retorna o comprimento/indicador para uma coluna segue o buffer para a coluna e precede o buffer para a próxima coluna. Esses campos são opcionais.  
  
 Quando o aplicativo solicita um novo conjunto de linhas, a biblioteca de cursores recupera dados de seu cache e do driver conforme necessário. Se os conjuntos de linhas novos e antigos se sobrepõem, a biblioteca de cursores pode otimizar seu desempenho reutilizando os dados das seções dos buffers de linhas sobrepostos. Portanto, as alterações não salvas os buffers de linhas são perdidas, a menos que se sobrepõem os conjuntos de linhas novos e antigos e as alterações nas seções a sobreposição dos buffers de linhas. Para salvar as alterações, um aplicativo envia uma instrução update posicionadas.  
  
 Observe que a biblioteca de cursores sempre atualiza os buffers de conjunto de linhas com dados do cache quando um aplicativo chama **SQLFetchScroll** com o *FetchOrientation* argumento definido como SQL_FETCH_RELATIVE e o *FetchOffset* argumento definido como 0.  
  
 A biblioteca de cursores dá suporte à chamada **SQLSetStmtAttr** com um *atributo* de SQL_ATTR_ROW_ARRAY_SIZE para alterar o tamanho do conjunto de linhas, enquanto um cursor é aberto. O novo tamanho do conjunto de linhas entrará em vigor na próxima vez que **SQLFetchScroll** é chamado.  
  
## <a name="result-set-membership"></a>Associação de conjunto de resultados  
 A biblioteca de cursores recupera dados do driver somente quando o aplicativo solicita a ele. Dependendo da fonte de dados e a configuração do atributo de instrução SQL_CONCURRENCY, isso tem as seguintes consequências:  
  
-   Os dados recuperados pela biblioteca de cursores podem diferir dos dados que estava disponíveis no momento em que a instrução foi executada. Por exemplo, após o cursor foi aberto, linhas inseridas em um ponto além da posição atual do cursor podem ser recuperadas por alguns drivers.  
  
-   Os dados no conjunto de resultados podem ser bloqueados pela fonte de dados para a biblioteca de cursor e, portanto, não estar disponível para outros usuários.  
  
 Depois que a biblioteca de cursores armazenou em cache uma linha de dados, ele não pode detectar alterações para aquela linha na fonte de dados subjacente (exceto atualizações posicionadas e exclusões operacional no cache do cursor mesmo). Isso ocorre porque, para chamadas para **SQLFetchScroll**, a biblioteca de cursores nunca refetches dados da fonte de dados. Em vez disso, ele refetches dados do seu cache.  
  
## <a name="scrolling"></a>Rolagem  
 A biblioteca de cursores suporta os seguintes tipos de busca em **SQLFetchScroll**.  
  
|Tipo de cursor|Tipos de busca|  
|-----------------|-----------------|  
|Somente avanço|SQL_FETCH_NEXT|  
|Estático|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>Erros  
 Quando **SQLFetchScroll** é chamado e uma das chamadas para **SQLFetch** retornará SQL_ERROR, os resultados da biblioteca de cursor da seguinte maneira. Depois de concluir essas etapas, a biblioteca de cursores continua o processamento.  
  
1.  Chamadas **SQLGetDiagRec** para obter informações de erro do driver e envia isso como um registro de diagnóstico no Gerenciador de Driver.  
  
2.  Define o campo SQL_DIAG_ROW_NUMBER no registro de diagnóstico para o valor apropriado.  
  
3.  Define o campo SQL_DIAG_COLUMN_NUMBER no registro de diagnóstico para o valor apropriado, se aplicável. Caso contrário, ele define como 0.  
  
4.  Define o valor para a linha de erro na matriz de status de linha para SQL_ROW_ERROR.  
  
 Após o cursor biblioteca chamou **SQLFetch** várias vezes em sua implementação de **SQLFetchScroll**, qualquer erro ou aviso retornado por uma das chamadas para **SQLFetch** estará em um registro de diagnóstico e pode ser recuperada por uma chamada para **SQLGetDiagRec**. Se os dados foram truncados quando ele foi encontrado, os dados truncados agora residirá no cache da biblioteca de cursor. As chamadas subsequentes para **SQLFetchScroll** para rolar até uma linha com dados truncados retornará os dados truncados e nenhum aviso será gerado porque os dados são buscados do cache da biblioteca de cursor. Para controlar o tamanho dos dados retornados para que ele possa determinar se os dados retornados em um buffer foi truncados, um aplicativo deve associar o buffer de comprimento/indicador.  
  
## <a name="bookmark-operations"></a>Operações de indicador  
 A biblioteca de cursores dá suporte à chamada **SQLFetchScroll** com um *FetchOrientation* de SQL_FETCH_BOOKMARK. Ele também suporta especificando um deslocamento de *FetchOffset* argumento pode ser usado na operação de indicador. Esta é a única operação de indicador que oferece suporte a biblioteca de cursores. A biblioteca de cursores não suporta chamada **SQLBulkOperations**.  
  
 Se o aplicativo definiu o atributo da instrução SQL_ATTR_USE_BOOKMARKS e tiver associado à coluna de indicador, a biblioteca de cursores gera um indicador de comprimento fixo e o retorna ao aplicativo. A biblioteca de cursores cria e mantém os indicadores que ele usa; Não use indicadores mantidas na fonte de dados. Quando **SQLFetchScroll** é chamado para recuperar um bloco de dados que já tiverem sido buscados da fonte de dados, ele recupera os dados do cache de biblioteca de cursor. Como resultado, o indicador é usado em uma chamada para **SQLFetchScroll** com um *FetchOrientation* de SQL_FETCH_BOOKMARK deve ser criado e mantido pela biblioteca de cursores.  
  
## <a name="interaction-with-other-functions"></a>Interação com outras funções  
 Um aplicativo deve chamar **SQLFetch** ou **SQLFetchScroll** antes de ele prepara ou executa qualquer posicionado instruções update ou delete.

