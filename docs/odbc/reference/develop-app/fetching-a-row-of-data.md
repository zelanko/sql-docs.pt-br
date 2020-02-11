---
title: Buscando uma linha de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], fetching a row of data
- cursors [ODBC], fetching rows
- result sets [ODBC], fetching
- fetches [ODBC], row of data
ms.assetid: 16d4a380-0d83-456b-aeee-f10738944e86
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 010d05990396c10836c0a2130e5d9f4392ae56ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069865"
---
# <a name="fetching-a-row-of-data"></a>Buscar uma linha de dados
Para buscar uma linha de dados, um aplicativo chama **SQLFetch**. **SQLFetch** pode ser chamado com qualquer tipo de cursor, mas move apenas o cursor do conjunto de linhas em uma direção somente de avanço. **SQLFetch** avança o cursor para a próxima linha e retorna os dados para todas as colunas que foram associadas a chamadas para **SQLBindCol**. Quando o cursor atinge o final do conjunto de resultados, **SQLFetch** retorna SQL_NO_DATA. Para obter exemplos de como chamar **SQLFetch**, consulte [usando SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 Exatamente como o **SQLFetch** é implementado é específico do driver, mas o padrão geral é que o driver recupere os dados para todas as colunas associadas da fonte de dados, converta-os de acordo com os tipos das variáveis associadas e coloque os dados convertidos nessas variáveis. Se o driver não puder converter nenhum dado, **SQLFetch** retornará um erro. O aplicativo pode continuar buscando linhas, mas os dados da linha atual são perdidos. O que acontece com os dados para colunas desassociadas depende do driver, mas a maioria dos drivers recupera e descarta ou nunca o recupera.  
  
 O driver também define os valores de todos os buffers de comprimento/indicador que foram associados. Se o valor de dados de uma coluna for nulo, o driver definirá o buffer de comprimento/indicador correspondente como SQL_NULL_DATA. Se o valor dos dados não for nulo, o driver definirá o buffer de comprimento/indicador como o comprimento de bytes dos dados após a conversão. Se esse comprimento não puder ser determinado, como às vezes é o caso com dados longos recuperados por mais de uma chamada de função, o driver define o buffer de comprimento/indicador como SQL_NO_TOTAL. Para tipos de dados de comprimento fixo, como inteiros e estruturas de data, o comprimento do byte é o tamanho do tipo de dados.  
  
 Para dados de comprimento variável, como dados de caracteres e binários, o driver verifica o tamanho de bytes dos dados convertidos em relação ao comprimento de bytes do buffer associado à coluna; o comprimento do buffer é especificado no argumento *BufferLength* em **SQLBindCol**. Se o comprimento de bytes dos dados convertidos for maior que o comprimento de bytes do buffer, o driver truncará os dados para caber no buffer, retornará o comprimento não truncado no buffer de comprimento/indicador, retornará SQL_SUCCESS_WITH_INFO e colocará o SQLSTATE 01004 (dados truncados) no diagnóstico. A única exceção a isso é se um indicador de comprimento variável é truncado quando retornado por **SQLFetch**, que retorna o SQLSTATE 22001 (dados da cadeia de caracteres, truncados à direita).  
  
 Os dados de comprimento fixo nunca são truncados, pois o driver pressupõe que o tamanho do buffer associado seja o tamanho do tipo de dados. O truncamento de dados tende a ser raro, pois o aplicativo geralmente associa um buffer grande o suficiente para manter todo o valor dos dados; Ele determina o tamanho necessário dos metadados. No entanto, o aplicativo pode associar explicitamente um buffer que ele sabe que é muito pequeno. Por exemplo, ele pode recuperar e exibir os primeiros 20 caracteres de uma descrição de parte ou os primeiros 100 caracteres de uma coluna de texto longo.  
  
 Os dados de caractere devem ser terminados com nulo pelo driver antes de serem retornados ao aplicativo, mesmo que tenham sido truncados. O caractere de terminação nula não está incluído no comprimento de bytes retornado, mas requer espaço no buffer associado. Por exemplo, suponha que um aplicativo use cadeias de caracteres compostas de dados de caractere no conjunto de caracteres ASCII, um driver tem 50 caracteres de dados a serem retornados e o buffer do aplicativo tem 25 bytes de comprimento. No buffer do aplicativo, o driver retorna os primeiros 24 caracteres seguidos de um caractere de terminação nula. No buffer de comprimento/indicador, ele retorna um comprimento de bytes de 50.  
  
 O aplicativo pode restringir o número de linhas no conjunto de resultados definindo o atributo de instrução SQL_ATTR_MAX_ROWS antes de executar a instrução que cria o conjunto de resultados. Por exemplo, o modo de visualização em um aplicativo usado para formatar relatórios precisa apenas de dados suficientes para exibir a primeira página do relatório. Ao restringir o tamanho do conjunto de resultados, esse recurso seria executado mais rapidamente. Este atributo de instrução destina-se a reduzir o tráfego de rede e pode não ter suporte de todos os drivers.
