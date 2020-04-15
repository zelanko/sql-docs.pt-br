---
title: Tipos de Descritores | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304887"
---
# <a name="types-of-descriptors"></a>Tipos de descritores
Um descritor é usado para descrever um dos seguintes:  
  
-   Um conjunto de parâmetros zero ou mais. Um descritor de parâmetros pode ser usado para descrever:  
  
    -   O *buffer de parâmetro de aplicativo,* que contém os argumentos dinâmicos de entrada definidos pelo aplicativo ou os argumentos dinâmicos de saída após a execução de uma declaração CALL de SQL. **CALL**  
  
    -   O *buffer de parâmetrode implementação*. Para argumentos dinâmicos de entrada, isso contém os mesmos argumentos do buffer de parâmetro do aplicativo, após qualquer conversão de dados que o aplicativo pode especificar. Para argumentos dinâmicos de saída, isso contém os argumentos retornados, antes de qualquer conversão de dados que o aplicativo possa especificar.  
  
     Para argumentos dinâmicos de entrada, o aplicativo deve operar em um descritor de parâmetro de aplicativo antes de executar qualquer declaração SQL que contenha marcadores de parâmetro dinâmicos. Para argumentos dinâmicos de entrada e saída, o aplicativo pode especificar diferentes tipos de dados daqueles no descritor de parâmetro de implementação para alcançar a conversão de dados.  
  
-   Uma única linha de dados do banco de dados. Um descritor de linha pode ser usado para descrever:  
  
    -   O *buffer de linha de implementação,* que contém a linha do banco de dados. (Esses buffers contêm conceitualmente dados escritos ou lidos no banco de dados. No entanto, a forma armazenada de dados do banco de dados não é especificada. Um banco de dados poderia realizar conversão adicional sobre os dados de sua forma no buffer de implementação.)  
  
    -   O *buffer de linha de aplicativo,* que contém a linha de dados apresentada ao aplicativo, segue qualquer conversão de dados que o aplicativo possa especificar.  
  
     O aplicativo opera no descritor da linha de aplicativo em qualquer caso em que os dados da coluna do banco de dados devem aparecer nas variáveis do aplicativo. Para obter a conversão de dados de dados de coluna, o aplicativo pode especificar diferentes tipos de dados daqueles do descritor da linha de implementação.  
  
 Os tipos de descritores são resumidos na tabela a seguir.  
  
|Tipo de buffer|Linhas|Parâmetros dinâmicos|  
|-----------------|----------|------------------------|  
|**Buffer de aplicativo**|Descritor de linha de aplicativo (ARD)|Descritor de parâmetro de aplicação (APD)|  
|**Buffer de implementação**|Descritor de linha de implementação (IRD)|Descritor de parâmetro de implementação (IPD)|  
  
 Para o parâmetro ou os buffers de linha, se o aplicativo especificar diferentes tipos de dados nos registros correspondentes da implementação e descritores de aplicativos, o driver realiza a conversão de dados quando usa os descritores. Por exemplo, ele pode converter valores numéricos e de data em formato de seqüência de caracteres. (Para conversões válidas, consulte [Apêndice D: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 Um descritor pode desempenhar diferentes funções. Diferentes declarações podem compartilhar qualquer descritor que o aplicativo aloca explicitamente. Um descritor de linha em uma declaração pode servir como um descritor de parâmetro em outra declaração.  
  
 Sabe-se sempre se um determinado descritor é um descritor de aplicativo ou um descritor de implementação, mesmo que o descritor ainda não tenha sido usado em uma operação de banco de dados. Para os descritores que a implementação aloca implicitamente, a implementação registra a linha predefinida em relação à alça da declaração. Qualquer descritor que o aplicativo aloca **chamando sqlAllocHandle** é um descritor de aplicativo.
