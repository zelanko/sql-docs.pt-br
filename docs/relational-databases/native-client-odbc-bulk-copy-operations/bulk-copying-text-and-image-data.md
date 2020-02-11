---
title: Cópia de dados de texto e imagem em massa | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ab694a8ba3a1976207ad1d0c6505cc953f39ff94
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73785148"
---
# <a name="bulk-copying-text-and-image-data"></a>Copiando em massa dados de texto e imagem
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Os valores de **texto**grande, **ntext**e **Image** são copiados em massa usando a função [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) . Você codifica [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para a coluna **Text**, **ntext**ou **Image** com um ponteiro *pData* definido como NULL, indicando que os dados serão fornecidos com **bcp_moretext**. É importante especificar o comprimento exato dos dados fornecidos para cada coluna **Text**, **ntext**ou **Image** em cada linha copiada em massa. Se o comprimento dos dados de uma coluna for diferente do comprimento da coluna especificado em [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md), use [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) para definir o comprimento como o valor adequado. Um [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) envia todos os dados que não são de**texto**, não**ntextos**e não de**imagem** ; em seguida, você chama **bcp_moretext** para enviar os dados **Text**, **ntext**ou **Image** em unidades separadas. As funções de cópia em massa determinam que todos os dados foram enviados para a coluna **Text**, **ntext**ou **Image** atual quando a soma dos comprimentos de dados enviados por meio de **bcp_moretext** é igual ao comprimento especificado no **bcp_collen** ou **bcp_bind**mais recente.  
  
 **bcp_moretext** não tem nenhum parâmetro para identificar uma coluna. Quando há várias colunas **Text**, **ntext**ou **image** em uma linha, **bcp_moretext** opera nas colunas **Text**, **ntext**ou **Image** , começando com a coluna que tem o número ordinal mais baixo e prosseguindo para a coluna com o número ordinal mais alto. **bcp_moretext** vai de uma coluna para a próxima quando a soma dos comprimentos de dados enviados for igual ao comprimento especificado no **bcp_collen** ou **bcp_bind** mais recente da coluna atual.  
  
## <a name="see-also"></a>Consulte Também  
 [Executando operações de cópia em massa &#40;&#41;ODBC](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
