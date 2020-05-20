---
title: Remodelar propriedade de nome-dinâmico (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Reshape Name property [ADO]
ms.assetid: 690229d1-46cc-42e6-a57d-4438251fe248
author: rothja
ms.author: jroth
ms.openlocfilehash: 490a69a022c2098de1dc4ade67af484b6e50131a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82756505"
---
# <a name="reshape-name-property-dynamic-ado"></a>Remodelar a propriedade dinâmica de nome (ADO)
Especifica um nome para o objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um valor de **cadeia de caracteres** que é o nome do **conjunto de registros**.  
  
## <a name="remarks"></a>Comentários  
 Os nomes persistem pela duração da conexão ou até que o **conjunto de registros** seja fechado.  
  
 A propriedade **nome de remodelação** destina-se principalmente ao recurso de remodelagem do [serviço de modelagem de dados da Microsoft para](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) o provedor de serviços OLE DB. Os nomes devem ser exclusivos para participar da nova formatação.  
  
 Essa propriedade é somente leitura, mas pode ser definida indiretamente quando um **conjunto de registros** é criado. Por exemplo, se uma cláusula de um comando de forma cria um **conjunto de registros** e fornece a ele um nome **de alias usando a palavra-** chave as, o alias é atribuído à propriedade nome de **remodelação** . Se nenhum alias for declarado, a propriedade **nome da forma** será atribuída a um nome exclusivo gerado pelo data Shaping Service. Se o nome do alias for igual ao nome de um conjunto de **registros**existente, nenhum **conjunto de registros** poderá ser remodelado até que um deles seja liberado. O comportamento padrão pode ser alterado definindo um nome exclusivo na propriedade [nome da forma](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md) na conexão ADO como **true**. Definir essa propriedade dá permissão ao serviço de modelagem de dados para alterar o nome atribuído pelo usuário, se necessário, para garantir a exclusividade. Para obter mais informações sobre a remodelagem, consulte [serviço de modelagem de dados da Microsoft para OLE DB (provedor de serviços ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md).  
  
 Use a propriedade **remodelar nome** quando desejar fazer referência a um **conjunto de registros** em um comando de forma ou quando você não souber o nome porque ele foi gerado pelo serviço de modelagem de dados. Nesse caso, você pode gerar um comando de forma concatenando o comando em volta da cadeia de caracteres retornada pela propriedade **nome da remodelação** .  
  
 **Remodelar nome** é uma propriedade dinâmica acrescentada à coleção de [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) do objeto **Recordset** quando a propriedade [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) é definida como **adUseClient**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Serviço de modelagem de dados da Microsoft para OLE DB (provedor de serviços ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [Comandos de forma em geral](../../../ado/guide/data/shape-commands-in-general.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
