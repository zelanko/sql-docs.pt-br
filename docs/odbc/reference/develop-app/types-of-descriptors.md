---
title: Tipos de descritores de | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], types
ms.assetid: ec20e446-e540-41ad-8559-d9c0a5b8358f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d9d4a7572131afeeb0017d3773b72d899052b32
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087789"
---
# <a name="types-of-descriptors"></a>Tipos de descritores
Um descritor é usado para descrever um dos seguintes:  
  
-   Um conjunto de zero ou mais parâmetros. Um descritor de parâmetro pode ser usado para descrever:  
  
    -   O *buffers de parâmetro de aplicativo,* que contém os entrada argumentos dinâmicos conforme definido pelo aplicativo ou os argumentos dinâmicos de saída após a execução de uma **chamar** instrução SQL.  
  
    -   O *buffers de parâmetro de implementação*. Para argumentos de entrada dinâmicos, isso contém os mesmos argumentos que o buffer de parâmetro de aplicativo, após o aplicativo pode especificar qualquer conversão de dados. Para argumentos de saída dinâmica, contém os argumentos retornados, antes de qualquer conversão de dados que o aplicativo pode especificar.  
  
     Para argumentos de entrada dinâmicos, o aplicativo deve funcionar em um descritor de parâmetro do aplicativo antes de executar qualquer instrução SQL que contém os marcadores de parâmetro dinâmico. Para argumentos de entrada e saídos dinâmicos, o aplicativo pode especificar os tipos de dados diferentes no descritor de parâmetro de implementação para fazer a conversão de dados.  
  
-   Uma única linha de dados do banco de dados. Um descritor de linha pode ser usado para descrever:  
  
    -   O *buffers de linha de implementação,* que contém a linha do banco de dados. (Esses buffers conceitualmente contêm dados como gravados ou leiam do banco de dados. No entanto, o formato armazenado do banco de dados não for especificado. Um banco de dados pode executar conversão adicional nos dados de sua forma no buffer de implementação.)  
  
    -   O *buffers de linha de aplicativo,* que contém a linha de dados como apresentado para o aplicativo, nenhuma conversão de dados que o aplicativo pode especificar a seguir.  
  
     O aplicativo opera com o descritor de linha de aplicativo em qualquer caso em que os dados da coluna do banco de dados devem aparecer em variáveis de aplicativo. Para fazer a conversão de dados de coluna de dados, o aplicativo pode especificar os tipos de dados diferentes no descritor de linha de implementação.  
  
 Os tipos de descritor são resumidos na tabela a seguir.  
  
|Tipo de buffer|Linhas|Parâmetros dinâmicos|  
|-----------------|----------|------------------------|  
|**Buffer de aplicativo**|descritor de linha de aplicativo (descartar)|parâmetro APD (descritor aplicativo)|  
|**Buffer de implementação**|descritor de linha de implementação (IRD)|descritor de parâmetro de implementação (IPD)|  
  
 Para o parâmetro ou os buffers de linha, se o aplicativo especifica os diferentes tipos de dados em registros correspondentes dos descritores de implementação e de aplicativo, o driver executa a conversão de dados quando ele usa os descritores. Por exemplo, ele pode converter valores numéricos e de data e hora para o formato de cadeia de caracteres. (Para conversões válidas, consulte [apêndice d: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 Um descritor pode executar diferentes funções. Instruções diferentes podem compartilhar qualquer descritor que o aplicativo aloca explicitamente. Um descritor de linha em uma instrução pode servir como um descritor de parâmetro em outra instrução.  
  
 Sempre é conhecido se um determinado descritor é um descritor de aplicativo ou um descritor de implementação, mesmo se o descritor de ainda não foi usado em uma operação de banco de dados. Para os descritores implicitamente aloca a implementação, a implementação grava a linha predefinida em relação ao identificador de instrução. Qualquer descritor que o aplicativo aloca chamando **SQLAllocHandle** é um descritor de aplicativo.
