---
title: Tipos de descritores | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a6c7b55194eb61c1a909ced2296e4ad2050b674
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304887"
---
# <a name="types-of-descriptors"></a>Tipos de descritores
Um descritor é usado para descrever um dos seguintes:  
  
-   Um conjunto de zero ou mais parâmetros. Um descritor de parâmetro pode ser usado para descrever:  
  
    -   O *buffer de parâmetro do aplicativo,* que contém os argumentos dinâmicos de entrada definidos pelo aplicativo ou os argumentos dinâmicos de saída após a execução de uma instrução de **chamada** do SQL.  
  
    -   O *buffer de parâmetro de implementação*. Para argumentos dinâmicos de entrada, ele contém os mesmos argumentos que o buffer de parâmetro de aplicativo, após qualquer conversão de dados que o aplicativo possa especificar. Para argumentos dinâmicos de saída, ele contém os argumentos retornados, antes de qualquer conversão de dados que o aplicativo possa especificar.  
  
     Para argumentos dinâmicos de entrada, o aplicativo deve operar em um descritor de parâmetro de aplicativo antes de executar qualquer instrução SQL que contenha marcadores de parâmetro dinâmico. Para argumentos dinâmicos de entrada e saída, o aplicativo pode especificar tipos de dados diferentes daqueles no descritor de parâmetro de implementação para obter a conversão de dados.  
  
-   Uma única linha de dados do banco de dado. Um descritor de linha pode ser usado para descrever:  
  
    -   O *buffer de linha de implementação,* que contém a linha do banco de dados. (Esses buffers conceitualmente contêm dados gravados ou lidos no banco de dado. No entanto, a forma armazenada de dados do banco de dado não é especificada. Um banco de dados pode executar uma conversão adicional nos dado de seu formulário no buffer de implementação.)  
  
    -   O *buffer de linha do aplicativo,* que contém a linha de dados conforme apresentado ao aplicativo, seguindo qualquer conversão de dados que o aplicativo possa especificar.  
  
     O aplicativo opera no descritor de linha do aplicativo em qualquer caso em que os dados da coluna do banco de dado devem aparecer nas variáveis do aplicativo. Para obter a conversão de dados de dados de coluna, o aplicativo pode especificar tipos de dados diferentes daqueles no descritor de linha de implementação.  
  
 Os tipos de descritores são resumidos na tabela a seguir.  
  
|Tipo de buffer|Linhas|Parâmetros dinâmicos|  
|-----------------|----------|------------------------|  
|**Buffer de aplicativo**|Descritor de linha de aplicativo (ARD)|Descritor de parâmetro de aplicativo (APD)|  
|**Buffer de implementação**|Descritor de linha de implementação (IRD)|Descritor de parâmetro de implementação (IPD)|  
  
 Para o parâmetro ou os buffers de linha, se o aplicativo especificar tipos de dados diferentes nos registros correspondentes da implementação e dos descritores de aplicativo, o driver executará a conversão de dados ao usar os descritores. Por exemplo, ele pode converter valores numéricos e DateTime em formato de cadeia de caracteres. (Para conversões válidas, consulte o [Apêndice D: tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 Um descritor pode executar funções diferentes. Instruções diferentes podem compartilhar qualquer descritor que o aplicativo aloca explicitamente. Um descritor de linha em uma instrução pode servir como um descritor de parâmetro em outra instrução.  
  
 É sempre conhecido se um determinado descritor é um descritor de aplicativo ou um descritor de implementação, mesmo que o descritor ainda não tenha sido usado em uma operação de banco de dados. Para os descritores que a implementação aloca implicitamente, a implementação registra a linha predefinida em relação ao identificador da instrução. Qualquer descritor que o aplicativo aloca ao chamar **SQLAllocHandle** é um descritor de aplicativo.
