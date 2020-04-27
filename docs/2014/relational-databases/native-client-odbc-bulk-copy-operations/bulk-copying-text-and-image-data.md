---
title: Cópia de dados de texto e imagem em massa | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c468ec3cf52526192893458055cde857aeaa864d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63067472"
---
# <a name="bulk-copying-text-and-image-data"></a>Copiando em massa dados de texto e imagem
  Os valores de **texto**grande, **ntext**e **Image** são copiados em massa usando a função [bcp_moretext](../native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) . Você codifica [bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para a coluna **Text**, **ntext**ou **Image** com um ponteiro *pData* definido como NULL, indicando que os dados serão fornecidos com **bcp_moretext**. É importante especificar o comprimento exato dos dados fornecidos para cada coluna **Text**, **ntext**ou **Image** em cada linha copiada em massa. Se o comprimento dos dados de uma coluna for diferente do comprimento da coluna especificado em [bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md), use [bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) para definir o comprimento como o valor adequado. Um [bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) envia todos os dados que não são de**texto**, não**ntextos**e não de**imagem** ; em seguida, você chama **bcp_moretext** para enviar os dados **Text**, **ntext**ou **Image** em unidades separadas. As funções de cópia em massa determinam que todos os dados foram enviados para a coluna **Text**, **ntext**ou **Image** atual quando a soma dos comprimentos de dados enviados por meio de **bcp_moretext** é igual ao comprimento especificado no **bcp_collen** ou **bcp_bind**mais recente.  
  
 **bcp_moretext** não tem nenhum parâmetro para identificar uma coluna. Quando há várias colunas **Text**, **ntext**ou **image** em uma linha, **bcp_moretext** opera nas colunas **Text**, **ntext**ou **Image** , começando com a coluna que tem o número ordinal mais baixo e prosseguindo para a coluna com o número ordinal mais alto. **bcp_moretext** vai de uma coluna para a próxima quando a soma dos comprimentos de dados enviados for igual ao comprimento especificado no **bcp_collen** ou **bcp_bind** mais recente da coluna atual.  
  
## <a name="see-also"></a>Consulte Também  
 [Executando operações de cópia em massa &#40;&#41;ODBC](performing-bulk-copy-operations-odbc.md)  
  
  
