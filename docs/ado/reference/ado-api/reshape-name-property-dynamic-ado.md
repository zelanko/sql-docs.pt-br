---
title: "Alterar o nome de propriedade dinâmica (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: Reshape Name property [ADO]
ms.assetid: 690229d1-46cc-42e6-a57d-4438251fe248
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8e18334a3e438ed484f24382e4a84f0a278747ea
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="reshape-name-property-dynamic-ado"></a>Alterar o nome de propriedade dinâmica (ADO)
Especifica um nome para o [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **cadeia de caracteres** valor que é o nome do **registros**.  
  
## <a name="remarks"></a>Remarks  
 Nomes de persistirem durante a conexão ou até que o **registros** está fechado.  
  
 O **nome remodelar** propriedade é usado principalmente para uso com o recurso de formatação novamente do [Microsoft Data Shaping Service para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) provedor de serviços. Nomes devem ser exclusivos para participar de formatação novamente.  
  
 Essa propriedade é somente leitura, mas pode ser definida indiretamente quando um **registros** é criado. Por exemplo, se uma cláusula de um comando de forma cria um **registros** e concede a ele um nome de alias usando o **AS** palavra-chave, o alias é atribuído ao **remodelar nome** propriedade. Se nenhum alias for declarado, o **nome remodelar** propriedade é atribuída um nome exclusivo gerado pelo data shaping service. Se o nome do alias é igual ao nome de um objeto existente **registros**, nem **registros** pode ser reformatado até que um deles seja liberado. O comportamento padrão pode ser alterado definindo um nome exclusivo no [nome remodelar](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md) propriedade sobre a conexão ADO para **True**. Definir esta propriedade fornece os dados de formatação para alterar o nome de usuário atribuído, se necessário, para garantir a exclusividade da permissão do serviço. Para obter mais informações sobre a reformulação das, consulte [Microsoft Data Shaping Service para OLE DB (provedor de serviços de ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md).  
  
 Use o **nome remodelar** propriedade quando você deseja se referir a um **registros** em um comando de forma, ou quando você não souber o nome, porque ele foi gerado pelo serviço de formatação de dados. Nesse caso, você pode gerar um comando de forma concatenando o comando em torno de cadeia de caracteres retornada pelo **nome remodelar** propriedade.  
  
 **Reformate nome** é uma propriedade dinâmica anexada ao **Recordset** do objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção quando o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) está definida como **adUseClient**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Microsoft Data Shaping Service para OLE DB (provedor de serviços de ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [Comandos de forma em geral](../../../ado/guide/data/shape-commands-in-general.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
