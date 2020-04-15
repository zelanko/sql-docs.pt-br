---
title: SQLFetchScroll (Biblioteca cursor) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e5573b8afc49afec8b7afa4fc52590e7a6a9e2fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302047"
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLFetchScroll** na biblioteca do cursor. Para obter informações gerais sobre **o SQLFetchScroll,** consulte [SQLFetchScroll Function](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
 A biblioteca do cursor implementa **o SQLFetchScroll** chamando repetidamente **sqlfetch** no driver. Ele transfere os dados que ele recupera do driver para os buffers de conjunto de linhas fornecidos pelo aplicativo. Ele também armazena os dados em arquivos de memória e disco. Quando um aplicativo solicita um novo conjunto de linhas, a biblioteca do cursor recupera-a conforme necessário do driver (se ele não tiver sido anteriormente buscado) ou do cache (se ele tiver sido anteriormente buscado). Finalmente, a biblioteca do cursor mantém o status dos dados armazenados em cache e retorna essas informações para o aplicativo na matriz de status da linha.  
  
 Quando a biblioteca do cursor é usada, as chamadas para **SQLFetchScroll** não podem ser misturadas com chamadas para **SQLFetch** ou **SQLExtendedFetch**.  
  
 Quando a biblioteca do cursor é usada, as chamadas para **SQLFetchScroll** são suportadas tanto para ODBC 2. *x* e para ODBC 3. *x* drivers.  
  
## <a name="rowset-buffers"></a>Buffers de conjunto de linhas  
 A biblioteca do cursor otimiza a transferência de dados do driver para o buffer de conjunto de linhas fornecido pelo aplicativo se:  
  
-   O aplicativo usa vinculação em termos de linha.  
  
-   Não há bytes não utilizados entre os campos na estrutura que o aplicativo declara conter uma linha de dados.  
  
-   Os campos nos quais **SQLFetch** ou **SQLFetchScroll** retorna o comprimento/indicador para uma coluna segue o buffer para essa coluna e precede o buffer para a próxima coluna. Esses campos são opcionais.  
  
 Quando o aplicativo solicita um novo conjunto de linhas, a biblioteca do cursor recupera dados de seu cache e do driver, conforme necessário. Se os conjuntos de linhas novos e antigos se sobreporem, a biblioteca do cursor pode otimizar seu desempenho reutilizando os dados das seções sobrepostas dos buffers de conjunto de linhas. Portanto, as alterações não salvas nos buffers do conjunto de linhas são perdidas a menos que os conjuntos de linhas novos e antigos se sobreponham e as alterações estejam nas seções sobrepostas dos buffers de conjunto de linhas. Para salvar as alterações, um aplicativo envia uma declaração de atualização posicionada.  
  
 Observe que a biblioteca do cursor sempre atualiza os buffers de conjunto de linhas com dados do cache quando um aplicativo chama **SQLFetchScroll** com o argumento *FetchOrientation* definido para SQL_FETCH_RELATIVE e o argumento *FetchOffset* definido como 0.  
  
 A biblioteca do cursor suporta chamar **SQLSetStmtAttr** com um *atributo* de SQL_ATTR_ROW_ARRAY_SIZE alterar o tamanho do conjunto de linhas enquanto um cursor está aberto. O novo tamanho do conjunto de linhas entrará em vigor na próxima vez que **o SQLFetchScroll** for chamado.  
  
## <a name="result-set-membership"></a>Associação conjunto de resultados  
 A biblioteca do cursor recupera dados do driver apenas conforme o aplicativo os solicita. Dependendo da fonte de dados e da configuração do atributo de declaração SQL_CONCURRENCY, isso tem as seguintes consequências:  
  
-   Os dados recuperados pela biblioteca do cursor podem diferir dos dados disponíveis no momento em que a declaração foi executada. Por exemplo, depois que o cursor foi aberto, as linhas inseridas em um ponto além da posição atual do cursor podem ser recuperadas por alguns drivers.  
  
-   Os dados no conjunto de resultados podem ser bloqueados pela fonte de dados da biblioteca do cursor e, portanto, indisponíveis para outros usuários.  
  
 Depois que a biblioteca do cursor tiver armazenado uma linha de dados em cache, ela não poderá detectar alterações nessa linha na fonte de dados subjacente (exceto para atualizações posicionadas e exclusões operando no cache do mesmo cursor). Isso ocorre porque, para chamadas ao **SQLFetchScroll,** a biblioteca do cursor nunca rebusca dados da fonte de dados. Em vez disso, ele rebusca dados de seu cache.  
  
## <a name="scrolling"></a>Rolagem  
 A biblioteca do cursor suporta os seguintes tipos de busca no **SQLFetchScroll**.  
  
|Tipo de cursor|Tipos de busca|  
|-----------------|-----------------|  
|Somente avanço|SQL_FETCH_NEXT|  
|Estático|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>Errors  
 Quando **o SQLFetchScroll** é chamado e uma das chamadas para **o SQLFetch** retorna SQL_ERROR, a biblioteca do cursor prossegue da seguinte forma. Depois de concluir essas etapas, a biblioteca do cursor continua a ser processada.  
  
1.  Chama **o SQLGetDiagRec** para obter informações de erro do motorista e posta isso como um registro de diagnóstico no Driver Manager.  
  
2.  Define o campo SQL_DIAG_ROW_NUMBER no registro diagnóstico para o valor apropriado.  
  
3.  Define o campo SQL_DIAG_COLUMN_NUMBER no registro diagnóstico ao valor adequado, se aplicável; caso contrário, ele define-lo para 0.  
  
4.  Define o valor da linha em erro na matriz de status da linha para SQL_ROW_ERROR.  
  
 Depois que a biblioteca do cursor tiver chamado **SQLFetch** várias vezes em sua implementação do **SQLFetchScroll,** qualquer erro ou aviso retornado por uma das chamadas para **o SQLFetch** estará em um registro de diagnóstico e poderá ser recuperado por uma chamada para **SQLGetDiagRec**. Se os dados foram truncados quando foram buscados, os dados truncados agora residirão no cache da biblioteca do cursor. Chamadas subseqüentes para **SQLFetchScroll** para rolar para uma linha com dados truncados retornarão os dados truncados, e nenhum aviso será levantado porque os dados são obtidos a partir do cache da biblioteca do cursor. Para acompanhar o comprimento dos dados retornados para que ele possa determinar se os dados retornados em um buffer foram truncados, um aplicativo deve vincular o buffer de comprimento/indicador.  
  
## <a name="bookmark-operations"></a>Operações de marcadores  
 A biblioteca do cursor suporta chamar **SQLFetchScroll** com uma *orientação* de SQL_FETCH_BOOKMARK. Ele também suporta especificar uma compensação no argumento *FetchOffset* que pode ser usado na operação de marcadores. Esta é a única operação de marcadores que a biblioteca do cursor suporta. A biblioteca do cursor não suporta chamar **SQLBulkOperations**.  
  
 Se o aplicativo tiver definido o atributo de declaração SQL_ATTR_USE_BOOKMARKS e estiver vinculado à coluna marcador, a biblioteca do cursor gerará um marcador de comprimento fixo e o devolverá ao aplicativo. A biblioteca do cursor cria e mantém os marcadores que usa; ele não usa marcadores mantidos na fonte de dados. Quando **o SQLFetchScroll** é chamado para recuperar um bloco de dados que já foi obtido na fonte de dados, ele recupera os dados do cache da biblioteca do cursor. Como resultado, o marcador usado em uma chamada para **SQLFetchScroll** com uma *Orientação de SQL_FETCH_BOOKMARK* deve ser criado e mantido pela biblioteca do cursor.  
  
## <a name="interaction-with-other-functions"></a>Interação com outras funções  
 Um aplicativo deve chamar **SQLFetch** ou **SQLFetchScroll** antes de preparar ou executar qualquer atualização posicionada ou excluir declarações.
