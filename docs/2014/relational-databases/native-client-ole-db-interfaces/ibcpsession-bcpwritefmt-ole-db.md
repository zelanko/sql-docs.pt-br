---
title: 'Ibcpsession:: Bcpwritefmt (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- IBCPSession::BCPWriteFmt (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPWriteFmt method
ms.assetid: add50425-2ed6-411a-a391-4ce63c364892
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 68be3cd9b1296ed1f9e3530c4aadcc5a28cea891
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37431045"
---
# <a name="ibcpsessionbcpwritefmt-ole-db"></a>IBCPSession::BCPWriteFmt (OLE DB)
  Grava informações de formato relativas a cada coluna no arquivo de formato.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT BCPWriteFmt(   
const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Remarks  
 O arquivo de formato especifica o formato de dados de um arquivo de dados criado por cópia em massa. Chamadas para o [ibcpsession:: BCPColumns](ibcpsession-bcpcolumns-ole-db.md) e [ibcpsession:: BCPColFmt](ibcpsession-bcpcolfmt-ole-db.md) métodos definem o formato do arquivo de dados. O método **BCPWriteFmt** salva essa definição no arquivo referenciado pelo argumento pwszFormatFile.  
  
 O método **BCPWriteFmt** pode salvar os arquivos de formato em xml ou formato de texto. Isso deve ser indicado usando o controle bcp_option_xml com o [ibcpsession:: Bcpcontrol](ibcpsession-bcpcontrol-ole-db.md) método.  
  
 Para carregar um arquivo de formato salvo, use o [ibcpsession:: Bcpreadfmt](ibcpsession-bcpreadfmt-ole-db.md) método.  
  
## <a name="arguments"></a>Argumentos  
 *pwszFormatFile*[in]  
 O caminho e o nome do arquivo que contém os valores de formato do arquivo de dados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método foi bem-sucedido.  
  
 E_FAIL  
 Ocorreu um erro específico do provedor; Para obter informações detalhadas, use o [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) interface.  
  
 E_OUTOFMEMORY  
 Erro de memória insuficiente.  
  
 E_UNEXPECTED  
 A chamada para o método era inesperada. Por exemplo, o [ibcpsession:: BCPInit](ibcpsession-bcpinit-ole-db.md) método não foi chamado antes de chamar esse método.  
  
## <a name="see-also"></a>Consulte também  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [Executando operações de cópia em massa](../native-client/features/performing-bulk-copy-operations.md)  
  
  
