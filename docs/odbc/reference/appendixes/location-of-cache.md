---
title: Local do Cache de | Microsoft Docs
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
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 240d6162-4da6-4b1f-96c7-f379f4ecb16f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b5798f94d1ac4d3c5f3132a955cd465e22ff0e19
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="location-of-cache"></a>Local do Cache
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 A biblioteca de cursores armazena em cache os dados na memória e nos arquivos temporários Windows®. Isso limita o tamanho do conjunto de resultados que a biblioteca de cursores pode manipular apenas por espaço em disco disponível. Um arquivo temporário é usado quando os dados sejam armazenados em cache seriam cruzar o limite de segmento se inserido no final do cache de biblioteca de cursor. Em vez disso, os dados sejam armazenados em cache são adicionados no lugar salvo por último bloco de dados no cache. O bloco de dados salvo por último é salvo em um arquivo temporário. Se a biblioteca de cursores encerrado de maneira anormal, como quando a energia falha, ele poderá deixar arquivos temporários do Windows no disco. Esses são denominados ~ CTT*nnnn*. tmp e são criados no diretório atual.  
  
> [!NOTE]  
>  Se a biblioteca de cursores no Microsoft® WindowsNT®/Windows2000 tentativas de cache de dados em um arquivo temporário no diretório atual, enquanto o aplicativo é executado de um compartilhamento somente leitura ou um CD (como um exemplo da biblioteca Microsoft Foundation Class), SQLSTATE HY000 (geral Error-Unable para criar um buffer de arquivo) será retornado.
