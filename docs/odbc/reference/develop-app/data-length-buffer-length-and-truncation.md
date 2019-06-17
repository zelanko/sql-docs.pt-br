---
title: Comprimento de dados, comprimento do Buffer e truncamento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- data length [ODBC]
- truncating data [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 2825c6e7-b9ff-42fe-84fc-7fb39728ac5d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ed2e5ca1fdaba97dde64329c5e8e1b692f43158
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267753"
---
# <a name="data-length-buffer-length-and-truncation"></a>Comprimento de dados, comprimento do buffer e truncamento
O *comprimento dos dados* é o comprimento de bytes dos dados como seriam armazenado no buffer de dados do aplicativo, não como ele é armazenado na fonte de dados. Essa distinção é importante porque os dados são geralmente armazenados em tipos diferentes no buffer de dados que na fonte de dados. Portanto, para os dados enviados à fonte de dados, esse é o comprimento de bytes dos dados antes da conversão em tipo da fonte de dados. Para os dados recuperados da fonte de dados, esse é o comprimento de bytes dos dados após a conversão para o tipo do buffer de dados e antes de qualquer truncamento é feito.  
  
 Para dados de comprimento fixo, como um inteiro ou uma estrutura de data, o tamanho de bytes dos dados é sempre o tamanho do tipo de dados. Em geral, aplicativos de alocar um buffer de dados que é o tamanho do tipo de dados. Se o aplicativo aloca um buffer menor, as consequências são indefinidas, porque o driver pressupõe que o buffer de dados é o tamanho do tipo de dados e não trunca os dados para se ajustar em um buffer menor. Se o aplicativo aloca um buffer maior, o espaço extra nunca é usado.  
  
 Para dados de comprimento variável, como caractere ou dados binários, é importante reconhecer que o tamanho de bytes dos dados é separada e muitas vezes diferente do que o comprimento de bytes do buffer. A relação entre esses dois tamanhos é descrita o [Buffers](../../../odbc/reference/develop-app/buffers.md) seção. Se o comprimento de bytes dos dados for maior que o comprimento de bytes do buffer, o driver trunca os dados buscados para o tamanho em bytes do buffer e retorna SQL_SUCCESS_WITH_INFO com SQLSTATE 01004 (dados truncados). No entanto, o comprimento de bytes retornada é o comprimento de dados completo.  
  
 Por exemplo, suponha que um aplicativo aloca 50 bytes para um buffer de dados binários. Se o driver tem 10 bytes de dados binários para retornar, ele retorna 10 bytes no buffer. O comprimento de bytes dos dados é 10 e o tamanho em bytes do buffer é 50. Se o driver tem 60 bytes de dados binários para retornar, ele trunca os dados para 50 bytes, retorna esses bytes no buffer e retorna SQL_SUCCESS_WITH_INFO. O comprimento de bytes dos dados é 60 (a duração antes do truncamento) e o tamanho em bytes do buffer ainda é 50.  
  
 Um registro de diagnóstico é criado para cada coluna que será truncada. Como demora para o driver a criar esses registros e para o aplicativo para processá-las, o truncamento pode prejudicar o desempenho. Normalmente, um aplicativo pode evitar esse problema ao alocar buffers grandes o suficiente, embora isso talvez não seja possível ao trabalhar com dados long. Quando ocorrer o truncamento de dados, o aplicativo, às vezes, pode alocar um buffer maior e buscar novamente os dados; Isso não é verdadeiro em todos os casos. Se ocorrer o truncamento durante a obtenção de dados com chamadas para **SQLGetData**, o aplicativo não precisa chamar **SQLGetData** para os dados que já foi retornados; para obter mais informações, consulte [Introdução Dados Long](../../../odbc/reference/develop-app/getting-long-data.md).
