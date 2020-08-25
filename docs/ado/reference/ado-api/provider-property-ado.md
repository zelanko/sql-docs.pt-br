---
description: Propriedade Provider (ADO)
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
ms.openlocfilehash: 8d96acadcd4b2df0eca5ff9655d9bcdd31cabe0f
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88772785"
---
# <a name="provider-property-ado"></a>Propriedade Provider (ADO)
Indica o nome do provedor para um objeto de [conexão](./connection-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **cadeia de caracteres** que indica o nome do provedor.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **Provider** para definir ou retornar o nome do provedor para uma conexão. Essa propriedade também pode ser definida pelo conteúdo da propriedade [ConnectionString](./connectionstring-property-ado.md) ou do argumento *ConnectionString* do método [Open](./open-method-ado-connection.md) ; no entanto, a especificação de um provedor em mais de um local ao chamar o método **Open** pode ter resultados imprevisíveis. Se nenhum provedor for especificado, a propriedade será padronizada para MSDASQL ([provedor Microsoft OLE DB para ODBC](../../guide/appendixes/microsoft-ole-db-provider-for-odbc.md)).  
  
 A propriedade do **provedor** é de leitura/gravação quando a conexão é fechada e somente leitura quando ela está aberta. A configuração não terá efeito até que você abra o objeto de **conexão** ou acesse a coleção [Propriedades](./properties-collection-ado.md) do objeto de **conexão** . Se a configuração não for válida, ocorrerá um erro.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Connection (ADO)](./connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades Provider e DefaultDatabase (VB)](./provider-and-defaultdatabase-properties-example-vb.md)   
 [Exemplo das propriedades Provider e DefaultDatabase (VB)](./provider-and-defaultdatabase-properties-example-vb.md)   
 [Provedor do Microsoft OLE DB para ODBC](../../guide/appendixes/microsoft-ole-db-provider-for-odbc.md)   
 [Apêndice A: Provedores](../../guide/appendixes/appendix-a-providers.md)