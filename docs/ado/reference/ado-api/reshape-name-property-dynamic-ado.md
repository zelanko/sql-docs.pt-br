---
title: Alterar a forma de nome de propriedade dinâmica (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f9b8898a3cc75cf47ae783a1dd2a120c8954ab8f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711659"
---
# <a name="reshape-name-property-dynamic-ado"></a>Remodelar a propriedade dinâmica de nome (ADO)
Especifica um nome para o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **cadeia de caracteres** valor que é o nome da **conjunto de registros**.  
  
## <a name="remarks"></a>Comentários  
 Nomes de manter para a duração da conexão ou até o **Recordset** está fechado.  
  
 O **nome remodelar** propriedade destina-se principalmente para uso com o recurso de formatação novamente do [Microsoft Data Shaping Service para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) provedor de serviços. Nomes devem ser exclusivos para participar de shaping novamente.  
  
 Essa propriedade é somente leitura, mas pode ser definida indiretamente quando um **Recordset** é criado. Por exemplo, se uma cláusula de um comando de forma cria uma **conjunto de registros** e concede a ele um nome de alias usando o **AS** palavra-chave, o alias é atribuído ao **remodelar nome** propriedade. Se nenhum alias for declarado, o **remodelar nome** propriedade é atribuída um nome exclusivo gerado pelo data shaping service. Se o nome do alias é igual ao nome de existente **conjunto de registros**, nem **Recordset** pode ser reformatado até que um deles seja liberado. O comportamento padrão pode ser alterado definindo um nome exclusivo na [nome remodelar](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md) propriedade sobre a conexão do ADO para **verdadeiro**. Definir essa propriedade fornece os dados shaping de permissão de serviço para alterar o nome de usuário atribuído, se necessário, para garantir a exclusividade. Para obter mais informações sobre a remodelagem, consulte [Microsoft Data Shaping Service para OLE DB (provedor de serviços do ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md).  
  
 Use o **nome remodelar** propriedade quando você deseja se referir a um **conjunto de registros** em um comando de forma, ou quando você não souber o nome porque ele foi gerado pelo Data Shaping Service. Nesse caso, você pode gerar um comando de forma concatenando o comando em torno de cadeia de caracteres retornada pela **remodelar nome** propriedade.  
  
 **Reformatar o nome** uma propriedade dinâmica que é acrescentada ao **conjunto de registros** do objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção quando o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) estiver definida como **adUseClient**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Microsoft Data Shaping Service para OLE DB (provedor de serviços do ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
