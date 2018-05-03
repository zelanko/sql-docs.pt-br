---
title: Propriedade do provedor (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 412a54f0a8028e14533a7e5bcb6a16f1911bcf14
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="provider-property-ado"></a>Propriedade do provedor (ADO)
Indica o nome do provedor para uma [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor que indica o nome do provedor.  
  
## <a name="remarks"></a>Remarks  
 Use o **provedor** propriedade para definir ou retornar o nome do provedor para uma conexão. Essa propriedade também pode ser definida pelo conteúdo do [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade ou o *ConnectionString* argumento do [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) método; porém, especificar um provedor em mais de um local ao chamar o **abrir** método pode ter resultados imprevisíveis. Se o provedor não for especificado, a propriedade padrão será MSDASQL ([Microsoft OLE DB Provider para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)).  
  
 O **provedor** propriedade é leitura/gravação quando a conexão é fechada e somente leitura quando ela é aberta. A configuração não terá efeito até que você abra o **Conexão** objeto ou acesso a [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção do **Conexão** objeto. Se a configuração não for válida, ocorrerá um erro.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades de DefaultDatabase (VB) e o provedor](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Exemplo de propriedades de DefaultDatabase (VB) e o provedor](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Provedor Microsoft OLE DB para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)   
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
