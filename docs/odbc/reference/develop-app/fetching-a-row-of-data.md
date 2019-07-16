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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069865"
---
# <a name="fetching-a-row-of-data"></a>Buscar uma linha de dados
Para buscar uma linha de dados, um aplicativo chama **SQLFetch**. **SQLFetch** podem ser chamados com qualquer tipo de cursor, mas ele só move o cursor de conjunto de linhas em uma direção de somente avanço. **SQLFetch** avança o cursor para a próxima linha e retorna os dados para todas as colunas que foram ligados com chamadas para **SQLBindCol**. Quando o cursor atinge o final do resultado definido, **SQLFetch** retorne SQL_NO_DATA. Para obter exemplos de chamada **SQLFetch**, consulte [usando SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 Exatamente como **SQLFetch** é implementada é específica do driver, mas em geral padrão é para o driver recuperar os dados para qualquer associar colunas da fonte de dados, convertê-lo de acordo com os tipos de variáveis associadas e coloque o dados convertidos nessas variáveis. Se o driver não é possível converter todos os dados, **SQLFetch** retornará um erro. O aplicativo pode continuar a busca de linhas, mas os dados para a linha atual serão perdidos. O que acontece com os dados para colunas não associadas depende do driver, mas a maioria dos drivers recuperar e descartá-lo ou recuperá-lo.  
  
 O driver também define os valores de qualquer comprimento/indicador de buffers de que tenham sido associados. Se o valor de dados para uma coluna for NULL, o driver define o buffer de comprimento/indicador correspondente como SQL_NULL_DATA. Se o valor de dados não for nulo, o driver define o buffer de comprimento/indicador para o tamanho de bytes dos dados após a conversão. Se esse comprimento não pode ser determinado, como, às vezes, é o caso com dados long são recuperados por mais de uma chamada de função, o driver definirá o buffer de comprimento/indicador como SQL_NO_TOTAL. Para tipos de dados de comprimento fixo, como inteiros e estruturas de data, o comprimento de bytes é o tamanho do tipo de dados.  
  
 Para dados de comprimento variável, como o caractere e dados binários, o driver verificará o comprimento de bytes dos dados convertidos com o tamanho de bytes do buffer associado à coluna; o comprimento do buffer é especificado na *BufferLength* argumento **SQLBindCol**. Se o comprimento de bytes dos dados convertidos for maior que o comprimento de bytes do buffer, o driver truncará os dados para caber no buffer, retorna o comprimento completo no buffer de comprimento/indicador, retorna SQL_SUCCESS_WITH_INFO e coloca o SQLSTATE 01004 (dados truncado) no diagnóstico. A única exceção a isso é se um indicador de comprimento variável será truncado quando retornado por **SQLFetch**, que retorna o SQLSTATE 22001 (dados de cadeia de caracteres, truncados à direita).  
  
 Dados de comprimento fixo nunca são truncados, pois o driver pressupõe que o tamanho do buffer associado é o tamanho do tipo de dados. Truncamento de dados tende a ser rara, pois o aplicativo geralmente está associado a um buffer grande o suficiente para conter o valor de dados inteiro; ele determina o tamanho necessário dos metadados. No entanto, o aplicativo pode associar explicitamente um buffer que ele saiba que pode para ser muito pequeno. Por exemplo, ele pode recuperar e exibir os primeiros 20 caracteres de uma descrição da parte ou os primeiros 100 caracteres de uma coluna de texto longo.  
  
 Dados de caractere devem ser terminada em nulo pelo driver antes de serem retornado para o aplicativo, mesmo se ele foi truncado. O caractere nulo de terminação não está incluído no comprimento de bytes retornada, mas requer espaço no buffer de associado. Por exemplo, suponha que um aplicativo usa cadeias de caracteres compostas de dados de caractere no conjunto de caracteres ASCII, um driver tem 50 caracteres de dados a serem retornados e o buffer do aplicativo é 25 bytes de comprimento. No buffer do aplicativo, o driver retorna os primeiro 24 caracteres seguidos por um caractere nulo de terminação. No buffer de comprimento/indicador, ele retorna um comprimento de byte de 50 caracteres.  
  
 O aplicativo pode restringir o número de linhas no conjunto de resultados por definindo o atributo da instrução SQL_ATTR_MAX_ROWS antes de executar a instrução que cria o resultado definido. Por exemplo, o modo de visualização em um aplicativo usado para formatar relatórios precisa apenas dados suficientes para exibir a primeira página do relatório. Restringindo o tamanho do conjunto de resultados, tal recurso seria executado mais rapidamente. Esse atributo de instrução tem como objetivo reduzir o tráfego de rede e não pode ter suporte por todos os drivers.
