---
title: Local do cache | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67990742"
---
# <a name="location-of-cache"></a>Local do cache
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 A biblioteca de cursores armazena em cache os dados na memória e no Windows® arquivos temporários. Isso limita o tamanho do conjunto de resultados que a biblioteca de cursores pode manipular somente por espaço em disco disponível. Um arquivo temporário é usado quando os dados a serem armazenados em cache cruzam o limite do segmento, se inserido no final do cache da biblioteca de cursores. Em vez disso, os dados a serem armazenados em cache são adicionados no lugar do último bloco de dados salvo no cache. O último bloco de dados salvo é salvo em um arquivo temporário. Se a biblioteca de cursores for encerrada de forma anormal, por exemplo, quando a energia falhar, ela poderá deixar os arquivos temporários do Windows no disco. Eles são chamados ~ CTT*nnnn*. tmp e são criados no diretório atual.  
  
> [!NOTE]  
>  Se a biblioteca de cursores no Microsoft®NT®/windows2000 tentar armazenar dados em cache em um arquivo temporário no diretório atual enquanto o aplicativo estiver sendo executado de um compartilhamento somente leitura ou um disco compacto (como um biblioteca MFC exemplo), SQLSTATE HY000 (erro geral-não é possível criar um buffer de arquivo) será retornado.
