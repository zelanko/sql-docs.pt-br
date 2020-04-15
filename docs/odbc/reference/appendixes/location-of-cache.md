---
title: Localização do Cache | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 13510332ae8bfab07a13d7831f9f74a048551214
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288614"
---
# <a name="location-of-cache"></a>Local do cache
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 A biblioteca do cursor armazena dados na memória e nos arquivos temporários ® Windows. Isso limita o tamanho do conjunto de resultados que a biblioteca do cursor pode lidar apenas com o espaço disponível em disco. Um arquivo temporário é usado quando os dados a serem armazenados em cache cruzariam o limite do segmento se inseridos no final do cache da biblioteca do cursor. Em vez disso, os dados a serem armazenados em cache são adicionados no lugar do último bloco de dados salvo no cache. O último bloco de dados salvo é salvo em um arquivo temporário. Se a biblioteca do cursor terminar de forma anormal, como quando a energia falha, ela pode deixar arquivos temporários do Windows no disco. Estes são chamados ~CTT*nnnn*.tmp e são criados no diretório atual.  
  
> [!NOTE]  
>  Se a biblioteca do cursor na Microsoft® WindowsNT®/Windows2000 tentar armazenar dados em um arquivo temporário no diretório atual enquanto o aplicativo estiver executando a partir de um compartilhamento somente leitura ou de um disco compacto (como uma amostra da Microsoft Foundation Class Library), o SQLSTATE HY000 (Geral Error-Unable para criar um buffer de arquivo) será devolvido.
