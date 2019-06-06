---
title: Propriedade Provider (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a8c571bf143d4aa68fc5785b91929635864e9ce8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702878"
---
# <a name="provider-property-ado"></a>Propriedade Provider (ADO)
Indica o nome do provedor para uma [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor que indica o nome do provedor.  
  
## <a name="remarks"></a>Comentários  
 Use o **provedor** propriedade para definir ou retornar o nome do provedor para uma conexão. Essa propriedade também pode ser definida pelo conteúdo do [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade ou o *ConnectionString* argumento do [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) método; no entanto, especificando um provedor em mais de um lugar durante a chamada a **abrir** método pode ter resultados imprevisíveis. Se nenhum provedor for especificado, a propriedade padrão será o MSDASQL ([Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)).  
  
 O **provedor** propriedade é leitura/gravação quando a conexão é fechada e somente leitura quando ele é aberto. A configuração não terá efeito até que você abra o **Conexão** objeto ou o acesso a [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção dos **Conexão** objeto. Se a configuração não for válida, ocorrerá um erro.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Provedor e o exemplo de propriedades de DefaultDatabase (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Provedor e o exemplo de propriedades de DefaultDatabase (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Provedor Microsoft OLE DB para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)   
 [Apêndice a: provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
