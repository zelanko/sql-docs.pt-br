---
title: Propriedade do provedor (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::get_Provider
- Connection15::PutProvider
- Connection15::put_Provider
- Connection15::GetProvider
- Connection15::Provider
helpviewer_keywords:
- Provider property [ADO]
ms.assetid: 0ff70e72-0061-4ffc-90fb-e3ea23129bb2
author: rothja
ms.author: jroth
ms.openlocfilehash: af95544a998963ffd81b4ebf9098089cc1a9915f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759902"
---
# <a name="provider-property-ado"></a>Propriedade Provider (ADO)
Indica o nome do provedor para um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **cadeia de caracteres** que indica o nome do provedor.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **Provider** para definir ou retornar o nome do provedor para uma conexão. Essa propriedade também pode ser definida pelo conteúdo da propriedade [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) ou do argumento *ConnectionString* do método [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) ; no entanto, a especificação de um provedor em mais de um local ao chamar o método **Open** pode ter resultados imprevisíveis. Se nenhum provedor for especificado, a propriedade será padronizada para MSDASQL ([provedor Microsoft OLE DB para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)).  
  
 A propriedade do **provedor** é de leitura/gravação quando a conexão é fechada e somente leitura quando ela está aberta. A configuração não terá efeito até que você abra o objeto de **conexão** ou acesse a coleção [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) do objeto de **conexão** . Se a configuração não for válida, ocorrerá um erro.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades Provider e DefaultDatabase (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Exemplo das propriedades Provider e DefaultDatabase (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Provedor do Microsoft OLE DB para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)   
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
