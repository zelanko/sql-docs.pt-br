---
title: Tipos de descritores de | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], types
ms.assetid: ec20e446-e540-41ad-8559-d9c0a5b8358f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5554b0d7d110db9270230c25ab2bcc29d5a7cb87
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="types-of-descriptors"></a>Tipos de descritores
Um descritor é usado para descrever um dos seguintes:  
  
-   Um conjunto de zero ou mais parâmetros. Um descritor de parâmetro pode ser usado para descrever:  
  
    -   O *buffers de parâmetro de aplicativo,* que contém os entrada argumentos dinâmicos conforme definido pelo aplicativo ou os argumentos dinâmicos de saída após a execução de um **chamar** instrução do SQL.  
  
    -   O *buffers de parâmetro de implementação*. Para argumentos de entrada dinâmicos, ela contém os mesmos argumentos que o buffer de parâmetro de aplicativo, após qualquer conversão de dados, que o aplicativo pode especificar. Para argumentos dinâmicos de saída, ela contém os argumentos retornados, antes de qualquer conversão de dados que o aplicativo pode especificar.  
  
     Para argumentos de entrada dinâmicos, o aplicativo deve funcionar em um descritor de parâmetro do aplicativo antes de executar qualquer instrução SQL que contém os marcadores de parâmetro dinâmico. Para argumentos de entrada e saídos dinâmicos, o aplicativo pode especificar os tipos de dados diferentes no descritor de parâmetro de implementação para alcançar a conversão de dados.  
  
-   Uma única linha de dados do banco de dados. Um descritor de linha pode ser usado para descrever:  
  
    -   O *buffers de linha de implementação,* que contém a linha do banco de dados. (Esses buffers conceitualmente contêm dados como escrito para ou de leitura do banco de dados. No entanto, o formulário armazenado do banco de dados não for especificado. Um banco de dados pode executar conversão adicional dos dados de forma no buffer de implementação.)  
  
    -   O *buffer de linhas de aplicativo,* que contém a linha de dados como apresentado para o aplicativo, nenhuma conversão de dados que o aplicativo pode especificar a seguir.  
  
     O aplicativo opera com o descritor de linha de aplicativo em qualquer caso em que os dados da coluna do banco de dados devem aparecer em variáveis de aplicativo. Para obter a conversão de dados de dados de coluna, o aplicativo pode especificar os tipos de dados diferentes no descritor de linha de implementação.  
  
 Os tipos de descritor são resumidos na tabela a seguir.  
  
|Tipo de buffer|Linhas|Parâmetros dinâmicos|  
|-----------------|----------|------------------------|  
|**Buffer de aplicativo**|Descritor de linha de aplicativo (descartar)|Descritor de parâmetro de aplicativo (APD)|  
|**Buffer de implementação**|Descritor de linha de implementação (IRD)|Descritor de parâmetro de implementação (IPD)|  
  
 Para o parâmetro ou os buffers de linha, se o aplicativo especificar tipos de dados diferentes em registros correspondentes dos descritores de implementação e o aplicativo, o driver executa a conversão de dados quando ele usa os descritores de. Por exemplo, ele pode converter valores numéricos e de data e hora para o formato de cadeia de caracteres. (Para conversões válidas, consulte [tipos de dados do apêndice d:](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 Um descritor pode executar diferentes funções. Instruções diferentes podem compartilhar qualquer descritor que o aplicativo aloca explicitamente. Um descritor de linha em uma instrução pode servir como um descritor de parâmetro em outra instrução.  
  
 Sempre é conhecido se um determinado descritor é um descritor de aplicativo ou um descritor de implementação, mesmo se o descritor ainda não foi usado em uma operação de banco de dados. Para os descritores de que a implementação aloca implicitamente, a implementação registra a linha predefinida em relação ao identificador de instrução. Nenhum descritor que o aplicativo aloca chamando **SQLAllocHandle** é um descritor de aplicativo.
