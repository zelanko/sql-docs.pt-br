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
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103826"
---
# <a name="bulk-copying-text-and-image-data"></a>Copiando em massa dados de texto e imagem
  Grandes **texto**, **ntext**, e **imagem** valores são copiados em massa usando o [bcp_moretext](../native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) função. Você codificar [bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para o **texto**, **ntext**, ou **imagem** coluna com um *pData* ponteiro definido como NULL indicando que os dados serão fornecidos com **bcp_moretext**. É importante especificar o comprimento exato de dados fornecidos para cada **texto**, **ntext**, ou **imagem** coluna em cada linha copiada em massa. Se o comprimento dos dados para uma coluna for diferente do comprimento da coluna especificado na [bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md), use [bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) para definir o comprimento para o valor adequado. Um [bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) envia todos os não -**texto**, não-**ntext**e não-**imagem** dados; você, em seguida, chamar **bcp_moretext** para enviar o **texto**, **ntext**, ou **imagem** dados em unidades separadas. Funções de cópia em massa determinam que todos os dados foram enviados para a atual **texto**, **ntext**, ou **imagem** coluna quando a soma dos comprimentos de dados enviados por meio de **bcp_moretext** é igual ao comprimento especificado no último **bcp_collen** ou **bcp_bind**.  
  
 **bcp_moretext** não tem nenhum parâmetro para identificar uma coluna. Quando houver vários **texto**, **ntext**, ou **imagem** colunas em uma linha **bcp_moretext** opera o **texto**, **ntext**, ou **imagem** colunas iniciando com a coluna com o número ordinal mais baixo e continuando para a coluna com o número ordinal mais alto. **bcp_moretext** vai de uma coluna para a próxima quando a soma dos comprimentos de dados enviados é igual ao comprimento especificado no último **bcp_collen** ou **bcp_bind** para a coluna atual.  
  
## <a name="see-also"></a>Consulte também  
 [Executando operações de cópia em massa &#40;ODBC&#41;](performing-bulk-copy-operations-odbc.md)  
  
  
