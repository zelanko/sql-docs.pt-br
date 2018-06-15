---
title: Cópia de dados de texto e imagem em massa | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5a8c6a70a4d1682117fff68cefe38f5d40a1e5d3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32944173"
---
# <a name="bulk-copying-text-and-image-data"></a>Copiando em massa dados de texto e imagem
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Grandes **texto**, **ntext**, e **imagem** os valores são copiados em massa usando o [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) função. Codificar [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para o **texto**, **ntext**, ou **imagem** coluna com um *pData* ponteiro definido como NULO indicando que os dados serão fornecidos com **bcp_moretext**. É importante especificar o comprimento exato dos dados fornecidos para cada **texto**, **ntext**, ou **imagem** coluna em cada linha copiada em massa. Se o comprimento dos dados de uma coluna for diferente do comprimento da coluna especificado em [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md), use [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) para definir o comprimento para o valor adequado. Um [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) envia todos os não -**texto**, não-**ntext**e não-**imagem** dados; em seguida, chame **bcp_moretext** para enviar o **texto**, **ntext**, ou **imagem** dados em unidades separadas. Funções de cópia em massa determinam que todos os dados foram enviados para a atual **texto**, **ntext**, ou **imagem** coluna quando a soma dos comprimentos de dados enviados por meio de **bcp_moretext** é igual ao comprimento especificado da última **bcp_collen** ou **bcp_bind**.  
  
 **bcp_moretext** não tem nenhum parâmetro para identificar uma coluna. Quando houver vários **texto**, **ntext**, ou **imagem** colunas em uma linha, **bcp_moretext** funciona com o **texto**, **ntext**, ou **imagem** colunas começando com a coluna com o número ordinal mais baixo e prosseguir para a coluna com o número ordinal mais alto. **bcp_moretext** vai de uma coluna para a próxima quando a soma dos comprimentos de dados enviados é igual ao comprimento especificado da última **bcp_collen** ou **bcp_bind** para a coluna atual.  
  
## <a name="see-also"></a>Consulte também  
 [Executando operações de cópia em massa &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
