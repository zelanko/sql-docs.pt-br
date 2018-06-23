---
title: Cópia de dados de texto e imagem em massa | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c674c24b4000ada4651dfb44ed2d49e9fd5bde83
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007943"
---
# <a name="bulk-copying-text-and-image-data"></a>Copiando em massa dados de texto e imagem
  Grandes **texto**, **ntext**, e **imagem** os valores são copiados em massa usando o [bcp_moretext](../native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) função. Codificar [bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para o **texto**, **ntext**, ou **imagem** coluna com um *pData* ponteiro definido como NULO indicando que os dados serão fornecidos com **bcp_moretext**. É importante especificar o comprimento exato dos dados fornecidos para cada **texto**, **ntext**, ou **imagem** coluna em cada linha copiada em massa. Se o comprimento dos dados de uma coluna for diferente do comprimento da coluna especificado em [bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md), use [bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) para definir o comprimento para o valor adequado. Um [bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) envia todos os não -**texto**, não-**ntext**e não-**imagem** dados; em seguida, chame **bcp_moretext** para enviar o **texto**, **ntext**, ou **imagem** dados em unidades separadas. Funções de cópia em massa determinam que todos os dados foram enviados para a atual **texto**, **ntext**, ou **imagem** coluna quando a soma dos comprimentos de dados enviados por meio de **bcp_moretext** é igual ao comprimento especificado da última **bcp_collen** ou **bcp_bind**.  
  
 **bcp_moretext** não tem nenhum parâmetro para identificar uma coluna. Quando houver vários **texto**, **ntext**, ou **imagem** colunas em uma linha, **bcp_moretext** funciona com o **texto**, **ntext**, ou **imagem** colunas começando com a coluna com o número ordinal mais baixo e prosseguir para a coluna com o número ordinal mais alto. **bcp_moretext** vai de uma coluna para a próxima quando a soma dos comprimentos de dados enviados é igual ao comprimento especificado da última **bcp_collen** ou **bcp_bind** para a coluna atual.  
  
## <a name="see-also"></a>Consulte também  
 [Executando operações de cópia em massa &#40;ODBC&#41;](performing-bulk-copy-operations-odbc.md)  
  
  