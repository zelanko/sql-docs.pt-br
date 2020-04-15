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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a702f561b756d5305020df9f015d3ea4b444caa6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305667"
---
# <a name="fetching-a-row-of-data"></a>Buscar uma linha de dados
Para buscar uma linha de dados, um aplicativo chama **SQLFetch**. **SQLFetch** pode ser chamado com qualquer tipo de cursor, mas ele só move o cursor do conjunto de linhas em uma direção somente para a frente. **O SQLFetch** avança o cursor para a próxima linha e retorna os dados para quaisquer colunas que foram vinculadas com chamadas para **SQLBindCol**. Quando o cursor chegar ao final do conjunto de resultados, o **SQLFetch** retorna SQL_NO_DATA. Para exemplos de chamada **SQLFetch,** consulte [Usando SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 Exatamente como o **SQLFetch** é implementado é específico do driver, mas o padrão geral é que o driver recupere os dados de quaisquer colunas vinculadas da fonte de dados, converta-os de acordo com os tipos das variáveis vinculadas e coloque os dados convertidos nessas variáveis. Se o driver não conseguir converter nenhum dado, **o SQLFetch** reahdeum erro. O aplicativo pode continuar buscando linhas, mas os dados da linha atual são perdidos. O que acontece com os dados para colunas não vinculadas depende do driver, mas a maioria dos motoristas ou recuperá-los e descartá-los ou nunca recuperá-los.  
  
 O driver também define os valores de quaisquer buffers de comprimento/indicador que tenham sido vinculados. Se o valor dos dados de uma coluna for NULO, o driver definirá o buffer de comprimento/indicador correspondente para SQL_NULL_DATA. Se o valor dos dados não for NULO, o driver definirá o buffer de comprimento/indicador para o comprimento do byte dos dados após a conversão. Se esse comprimento não puder ser determinado, como às vezes é o caso com dados longos que são recuperados por mais de uma chamada de função, o driver define o buffer de comprimento/indicador para SQL_NO_TOTAL. Para tipos de dados de comprimento fixo, como inteiros e estruturas de data, o comprimento do byte é o tamanho do tipo de dados.  
  
 Para dados de comprimento variável, como dados de caracteres e binários, o driver verifica o comprimento do byte dos dados convertidos em relação ao comprimento do byte do buffer vinculado à coluna; o comprimento do buffer é especificado no argumento *BufferLength* no **SQLBindCol**. Se o comprimento do byte dos dados convertidos for maior do que o comprimento do byte do buffer, o driver truncaros os dados para caber no buffer, retornar o comprimento não truncado no buffer de comprimento/indicador, retornar SQL_SUCCESS_WITH_INFO e colocar SQLSTATE 01004 (Dados truncados) nos diagnósticos. A única exceção a isso é se um marcador de comprimento variável for truncado quando devolvido pelo **SQLFetch**, que retorna SQLSTATE 22001 (dados string, truncados à direita).  
  
 Os dados de comprimento fixo nunca são truncados, porque o driver assume que o tamanho do buffer bound é o tamanho do tipo de dados. A truncação de dados tende a ser rara, pois o aplicativo geralmente vincula um buffer grande o suficiente para manter todo o valor dos dados; ele determina o tamanho necessário a partir dos metadados. No entanto, o aplicativo pode explicitamente vincular um buffer que ele sabe ser muito pequeno. Por exemplo, ele pode recuperar e exibir os primeiros 20 caracteres de uma descrição de peça ou os primeiros 100 caracteres de uma longa coluna de texto.  
  
 Os dados de caracteres devem ser anulados pelo motorista antes de serem devolvidos ao aplicativo, mesmo que tenha sido truncado. O caractere de rescisão nula não está incluído no comprimento do byte retornado, mas requer espaço no buffer vinculado. Por exemplo, suponha que um aplicativo use strings compostas de dados de caracteres no conjunto de caracteres ASCII, um driver tem 50 caracteres de dados para retornar e o buffer do aplicativo tem 25 bytes de comprimento. No buffer do aplicativo, o driver retorna os primeiros 24 caracteres seguidos de um caractere de rescisão nula. No buffer de comprimento/indicador, ele retorna um comprimento de byte de 50.  
  
 O aplicativo pode restringir o número de linhas no resultado definido definindo o atributo de declaração SQL_ATTR_MAX_ROWS antes de executar a declaração que cria o conjunto de resultados. Por exemplo, o modo de visualização em um aplicativo usado para formatar relatórios precisa apenas de dados suficientes para exibir a primeira página do relatório. Ao restringir o tamanho do conjunto de resultados, tal recurso seria executado mais rápido. Este atributo de declaração destina-se a reduzir o tráfego de rede e pode não ser suportado por todos os motoristas.
