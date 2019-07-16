---
title: Local do Cache | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 240d6162-4da6-4b1f-96c7-f379f4ecb16f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a925b66b0d09a9beb32e4441d62bc4fa9296313
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990742"
---
# <a name="location-of-cache"></a>Local do cache
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 A biblioteca de cursores armazena em cache dados na memória e nos arquivos temporários do Windows®. Isso limita o tamanho do conjunto de resultados que a biblioteca de cursores pode manipular apenas pelo espaço em disco disponível. Um arquivo temporário é usado quando os dados sejam armazenados em cache seriam cruzar o limite de segmento se inseridos no final do cache de biblioteca de cursor. Em vez disso, os dados sejam armazenados em cache são adicionados no lugar do bloco de última salva dados no cache. O bloco de dados salvo por último é salvo em um arquivo temporário. Se a biblioteca de cursores terminar de maneira anormal, como quando a alimentação falha, ele pode deixar os arquivos temporários no disco do Windows. Esses são denominados ~ CTT*nnnn*. tmp e são criados no diretório atual.  
  
> [!NOTE]  
>  Se a biblioteca de cursores no Microsoft® WindowsNT®/Windows2000 tentativas em cache os dados em um arquivo temporário no diretório atual, enquanto o aplicativo é executado de um compartilhamento somente leitura ou um disco de CD (como um exemplo da biblioteca Microsoft Foundation Class), SQLSTATE HY000 (geral Error-Unable para criar um buffer de arquivo) será retornado.
