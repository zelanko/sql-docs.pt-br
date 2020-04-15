---
title: Comprimento de dados, comprimento do buffer e truncação | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2e7b8d1e60cd83594509c2ab5cbc24e04546eca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305221"
---
# <a name="data-length-buffer-length-and-truncation"></a>Comprimento de dados, comprimento do buffer e truncamento
O *comprimento dos dados* é o comprimento do byte dos dados, pois seria armazenado no buffer de dados do aplicativo, não como ele é armazenado na fonte de dados. Essa distinção é importante porque os dados são muitas vezes armazenados em diferentes tipos no buffer de dados do que na fonte de dados. Assim, para os dados que estão sendo enviados para a fonte de dados, este é o comprimento do byte dos dados antes da conversão para o tipo de fonte de dados. Para os dados que estão sendo recuperados da fonte de dados, este é o comprimento do byte dos dados após a conversão para o tipo de buffer de dados e antes que qualquer truncamento seja feito.  
  
 Para dados de comprimento fixo, como um inteiro ou uma estrutura de data, o comprimento do byte dos dados é sempre o tamanho do tipo de dados. Em geral, os aplicativos alocam um buffer de dados que é o tamanho do tipo de dados. Se o aplicativo alocar um buffer menor, as consequências serão indefinidas porque o driver assume que o buffer de dados é do tamanho do tipo de dados e não trunca os dados para se encaixar em um buffer menor. Se o aplicativo alocar um buffer maior, o espaço extra nunca será usado.  
  
 Para dados de comprimento variável, como dados de caracteres ou binários, é importante reconhecer que o comprimento do byte dos dados é separado e muitas vezes diferente do comprimento do byte do buffer. A relação desses dois comprimentos é descrita na seção [Buffers.](../../../odbc/reference/develop-app/buffers.md) Se o comprimento do byte dos dados for maior do que o comprimento do byte do buffer, o driver trunca dados buscados até o comprimento do byte do buffer e retorna SQL_SUCCESS_WITH_INFO com SQLSTATE 01004 (Dados truncados). No entanto, o comprimento do byte retornado é o comprimento dos dados não truncados.  
  
 Por exemplo, suponha que um aplicativo aloque 50 bytes para um buffer de dados binário. Se o driver tiver 10 bytes de dados binários para retornar, ele retorna esses 10 bytes no buffer. O comprimento do byte dos dados é de 10, e o comprimento do byte do buffer é de 50. Se o driver tiver 60 bytes de dados binários para retornar, ele trunca os dados para 50 bytes, devolve esses bytes no buffer e retorna SQL_SUCCESS_WITH_INFO. O comprimento do byte dos dados é de 60 (o comprimento antes da truncação), e o comprimento do byte do buffer ainda é de 50.  
  
 Um registro de diagnóstico é criado para cada coluna truncada. Como leva tempo para o motorista criar esses registros e para o aplicativo processá-los, a truncação pode degradar o desempenho. Normalmente, um aplicativo pode evitar esse problema alocando buffers grandes o suficiente, embora isso possa não ser possível ao trabalhar com dados longos. Quando ocorre a truncação de dados, o aplicativo às vezes pode alocar um buffer maior e rebuscar os dados; isso não é verdade em todos os casos. Se a truncação ocorrer ao receber dados com chamadas para **SQLGetData,** o aplicativo não precisa chamar **SQLGetData** para obter dados que já foram retornados; para obter mais informações, consulte [Getting Long Data](../../../odbc/reference/develop-app/getting-long-data.md).
