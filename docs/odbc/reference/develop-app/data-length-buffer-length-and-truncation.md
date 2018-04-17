---
title: Comprimento de dados, o tamanho do Buffer e o truncamento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data buffers [ODBC], length
- data length [ODBC]
- truncating data [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 2825c6e7-b9ff-42fe-84fc-7fb39728ac5d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f6934769c4f78063e24a393877112c2219121740
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="data-length-buffer-length-and-truncation"></a>Comprimento de dados, o tamanho do Buffer e o truncamento
O *comprimento dos dados* é o comprimento de bytes dos dados como ele deve ser armazenado em buffer de dados do aplicativo, não como ele é armazenado na fonte de dados. Essa distinção é importante porque os dados geralmente são armazenados em tipos diferentes no buffer de dados na fonte de dados. Assim, para dados enviados para a fonte de dados, isso é o comprimento de bytes dos dados antes da conversão em tipo de fonte de dados. Para os dados recuperados da fonte de dados, esse é o comprimento de bytes dos dados após a conversão para tipo de buffer de dados e antes de qualquer truncamento é feito.  
  
 Para dados de comprimento fixo, como um número inteiro ou uma estrutura de data, o comprimento de bytes dos dados é sempre o tamanho do tipo de dados. Em geral, os aplicativos de alocar um buffer de dados que é o tamanho do tipo de dados. Se o aplicativo aloca um buffer menor, as consequências são indefinidas porque o driver pressupõe que o buffer de dados é o tamanho do tipo de dados e não trunca os dados para se ajustar em um buffer menor. Se o aplicativo aloca um buffer maior, o espaço extra nunca é usado.  
  
 Para dados de comprimento variável, como caractere ou dados binários, é importante reconhecer que o comprimento de bytes dos dados é separado do e geralmente diferente do que o comprimento de bytes do buffer. A relação entre esses dois comprimentos descrita o [Buffers](../../../odbc/reference/develop-app/buffers.md) seção. Se o comprimento de bytes dos dados for maior que o comprimento de bytes do buffer, o driver trunca os dados buscados para o comprimento de bytes do buffer e retorna SQL_SUCCESS_WITH_INFO com SQLSTATE 01004 (dados truncados). No entanto, o comprimento de bytes retornados é o comprimento de dados completo.  
  
 Por exemplo, suponha que um aplicativo aloca 50 bytes para um buffer de dados binários. Se o driver tem 10 bytes de dados binários a serem retornados, ele retorna 10 bytes no buffer. O comprimento de bytes dos dados é 10 e o comprimento de bytes do buffer é 50. Se o driver tem 60 bytes de dados binários a serem retornados, truncará os dados para 50 bytes, retorna os bytes no buffer e retorna SQL_SUCCESS_WITH_INFO. O comprimento de bytes dos dados é 60 (comprimento antes de truncamento) e o comprimento de bytes do buffer ainda é 50.  
  
 Um registro de diagnóstico é criado para cada coluna que será truncada. Porque o tempo necessário para o driver a criar esses registros e para o aplicativo para processá-las, o truncamento pode prejudicar o desempenho. Normalmente, um aplicativo pode evitar esse problema ao alocar buffers grandes o suficiente, embora isso talvez não seja possível ao trabalhar com dados long. Quando ocorrer o truncamento de dados, o aplicativo pode, às vezes, aloque um buffer maior e buscar novamente os dados. Isso não é verdadeiro em todos os casos. Se ocorrer um truncamento durante a obtenção de dados com chamadas para **SQLGetData**, o aplicativo não precisa chamar **SQLGetData** para dados que já foi retornados; para obter mais informações, consulte [obtendo Dados Long](../../../odbc/reference/develop-app/getting-long-data.md).
