---
title: Comprimento dos dados, comprimento do buffer e truncamento | Microsoft Docs
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
ms.openlocfilehash: 8586157237db1158587e3c39f1320b78d8251fb5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081474"
---
# <a name="data-length-buffer-length-and-truncation"></a>Comprimento de dados, comprimento do buffer e truncamento
O *comprimento dos dados* é o comprimento de bytes dos dados, pois ele seria armazenado no buffer de dados do aplicativo, não como ele é armazenado na fonte de dados. Essa distinção é importante porque os dados geralmente são armazenados em tipos diferentes no buffer de dados do que na fonte de dados. Portanto, para dados enviados para a fonte de dados, esse é o comprimento de bytes dos dados antes da conversão para o tipo da fonte de dados. Para os dados que estão sendo recuperados da fonte de dados, esse é o comprimento de bytes dos dados após a conversão para o tipo do buffer de dados e antes de qualquer truncamento ser feito.  
  
 Para dados de comprimento fixo, como um inteiro ou uma estrutura de data, o comprimento de bytes dos dados é sempre o tamanho do tipo de dados. Em geral, os aplicativos alocam um buffer de dados que é o tamanho do tipo de dados. Se o aplicativo alocar um buffer menor, as consequências serão indefinidas porque o driver assume que o buffer de dados é o tamanho do tipo de dados e não trunca os dados para caber em um buffer menor. Se o aplicativo alocar um buffer maior, o espaço extra nunca será usado.  
  
 Para dados de comprimento variável, como dados de caracteres ou binários, é importante reconhecer que o comprimento de bytes dos dados é separado e, muitas vezes, diferente do comprimento de bytes do buffer. A relação desses dois comprimentos é descrita na seção [buffers](../../../odbc/reference/develop-app/buffers.md) . Se o comprimento de bytes dos dados for maior que o comprimento de bytes do buffer, o driver truncará os dados buscados para o comprimento de bytes do buffer e retornará SQL_SUCCESS_WITH_INFO com SQLSTATE 01004 (dados truncados). No entanto, o comprimento de bytes retornado é o comprimento dos dados não truncados.  
  
 Por exemplo, suponha que um aplicativo aloque 50 bytes para um buffer de dados binários. Se o driver tiver 10 bytes de dados binários para retornar, ele retornará esses 10 bytes no buffer. O comprimento de bytes dos dados é 10 e o comprimento de bytes do buffer é 50. Se o driver tiver 60 bytes de dados binários para retornar, ele truncará os dados para 50 bytes, retornará esses bytes no buffer e retornará SQL_SUCCESS_WITH_INFO. O comprimento de bytes dos dados é 60 (o comprimento antes do truncamento) e o comprimento de bytes do buffer ainda é 50.  
  
 Um registro de diagnóstico é criado para cada coluna truncada. Como leva tempo para o driver criar esses registros e para que o aplicativo processá-los, o truncamento pode prejudicar o desempenho. Normalmente, um aplicativo pode evitar esse problema alocando buffers grandes o suficiente, embora isso possa não ser possível ao trabalhar com dados longos. Quando ocorre um truncamento de dados, às vezes o aplicativo pode alocar um buffer maior e buscar novamente os dados; Isso não é verdade em todos os casos. Se o truncamento ocorrer ao obter dados com chamadas para **SQLGetData**, o aplicativo não precisará chamar **SQLGetData** para dados que já foram retornados; para obter mais informações, consulte [obtendo dados longos](../../../odbc/reference/develop-app/getting-long-data.md).
