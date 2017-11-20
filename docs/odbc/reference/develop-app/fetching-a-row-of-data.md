---
title: Busca de uma linha de dados | Microsoft Docs
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
- SQLFetch function [ODBC], fetching a row of data
- cursors [ODBC], fetching rows
- result sets [ODBC], fetching
- fetches [ODBC], row of data
ms.assetid: 16d4a380-0d83-456b-aeee-f10738944e86
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 142c9a2c95900e5b3776f96d86a145defc447512
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="fetching-a-row-of-data"></a>Busca de uma linha de dados
Para buscar uma linha de dados, um aplicativo chama **SQLFetch**. **SQLFetch** pode ser chamado com qualquer tipo de cursor, mas ele só move o cursor de conjunto de linhas em uma direção de somente avanço. **SQLFetch** avança o cursor para a próxima linha e retorna os dados de todas as colunas que foram associados com chamadas para **SQLBindCol**. Quando o cursor atinge o final do resultado definido, **SQLFetch** retorna SQL_NO_DATA. Para obter exemplos de chamada **SQLFetch**, consulte [SQLBindCol usando](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 Exatamente como **SQLFetch** é implementado é específica do driver, mas em geral é padrão para o driver recuperar os dados para qualquer associar colunas da fonte de dados, convertê-la de acordo com os tipos de variáveis associadas e coloque o dados convertidos dessas variáveis. Se o driver não pode converter todos os dados, **SQLFetch** retornará um erro. O aplicativo pode continuar a busca de linhas, mas os dados para a linha atual serão perdidos. O que acontece com os dados para colunas desassociadas depende do driver, mas a maioria dos drivers recuperar e descartá-lo ou recuperá-lo.  
  
 O driver também define os valores de buffers de comprimento/indicador tem sido vinculados. Se o valor dos dados para uma coluna for NULL, o driver define o buffer de comprimento/indicador correspondente como SQL_NULL_DATA. Se o valor de dados não for NULL, o driver define o buffer de comprimento/indicador para o comprimento de bytes de dados após a conversão. Se esse comprimento não pode ser determinado, como às vezes é o caso com dados long são recuperados por mais de uma chamada de função, o driver define o buffer de comprimento/indicador para SQL_NO_TOTAL. Para tipos de dados de comprimento fixo, como números inteiros e estruturas de data, o comprimento em bytes é o tamanho do tipo de dados.  
  
 Para dados de comprimento variável, como caractere e dados binários, o driver verifica o comprimento de bytes dos dados convertidos contra o comprimento de bytes do buffer associado à coluna; o comprimento do buffer especificado no *BufferLength* argumento **SQLBindCol**. Se o comprimento de bytes dos dados convertidos for maior que o comprimento de bytes do buffer, o driver truncará os dados para se ajustar no buffer e retorna o comprimento completo no buffer de comprimento/indicador, retorna SQL_SUCCESS_WITH_INFO e coloca o SQLSTATE 01004 (dados truncado) no diagnóstico. A única exceção a isso é se um indicador de comprimento variável será truncado quando retornado por **SQLFetch**, que retorna o SQLSTATE 22001 (dados de cadeia de caracteres, truncados à direita).  
  
 Dados de comprimento fixo nunca são truncados, pois o driver pressupõe que o tamanho do buffer associado é o tamanho do tipo de dados. Truncamento de dados tende a ser raros, porque o aplicativo geralmente associa um buffer grande o suficiente para conter o valor de inteiro de dados; Determina o tamanho necessário dos metadados. No entanto, o aplicativo pode associar explicitamente um buffer que ele saiba que pode ser muito pequeno. Por exemplo, ele pode recuperar e exibir os primeiros 20 caracteres de uma descrição de parte ou os 100 primeiros caracteres de uma coluna de texto longo.  
  
 Dados de caractere devem ser terminada em nulo pelo driver antes de ser retornado para o aplicativo, mesmo se ele foi truncado. O caractere null de terminação não está incluído no comprimento de bytes retornados, mas requer espaço no buffer de associados. Por exemplo, suponha que um aplicativo usa cadeias de caracteres compostas de dados de caractere no conjunto de caracteres ASCII, um driver tem 50 caracteres de dados para retornar e o buffer do aplicativo é 25 bytes de comprimento. No buffer do aplicativo, o driver retorna os primeiro 24 caracteres seguidos por um caractere null de terminação. No buffer de comprimento/indicador, ele retorna um comprimento de bytes de 50.  
  
 O aplicativo pode restringir o número de linhas no conjunto de resultados por definir o atributo de instrução SQL_ATTR_MAX_ROWS antes de executar a instrução que cria o resultado definido. Por exemplo, o modo de visualização em um aplicativo usado para formatar relatórios precisa apenas dados suficientes para exibir a primeira página do relatório. Restringindo o tamanho do conjunto de resultados, tal recurso seria executado mais rapidamente. Esse atributo de instrução destina-se para reduzir o tráfego de rede e pode não ter suporte de todos os drivers.

