---
title: Propriedade ActiveConnection (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ActiveConnection
- Cellset::ActiveConnection
- Catalog::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO MD]
ms.assetid: 2509b32c-a995-4364-9152-d8c83129bdd8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6ad7cdfdfc3c08175faf0584f2ae5069fcd39acb
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719016"
---
# <a name="activeconnection-property-ado-md"></a>Propriedade ActiveConnection (ADO MD)
Indica para qual ADO [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) o conjunto de células atual do objeto ou catálogo ao qual pertence atualmente.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **Variant** que contém uma cadeia de caracteres que define uma conexão ou **Conexão** objeto. O padrão é vazio.  
  
## <a name="remarks"></a>Comentários  
 Você pode definir essa propriedade para um válido ADO **Conexão** objeto ou uma cadeia de caracteres de conexão válida. Quando essa propriedade é definida como uma cadeia de caracteres de conexão, o provedor cria uma nova **Conexão** usando esta definição de objeto e abre a conexão.  
  
 Se você usar o *ActiveConnection* argumento do [abra](../../../ado/reference/ado-md-api/open-method-ado-md.md) método para abrir um [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto, o **ActiveConnection** será de propriedade herde o valor do argumento.  
  
 Definindo o **ActiveConnection** propriedade de uma [catálogo](../../../ado/reference/ado-md-api/catalog-object-ado-md.md) objeto **nada** libera os dados associados, inclusive dados no [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) coleta e qualquer um relacionado [dimensão](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [hierarquia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md), e [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objetos. Fechando uma **Conexão** objeto que foi usado para abrir um **catálogo** tem o mesmo efeito que definir a **ActiveConnection** propriedade **nada**.  
  
 Alterando o banco de dados padrão da conexão referenciada pela **ActiveConnection** propriedade de uma **catálogo** objeto invalida o conteúdo do **catálogo**.  
  
 Um erro ocorrerá se você tentar alterar o **ActiveConnection** propriedade para que a abertura **conjunto de células** objeto.  
  
> [!NOTE]
>  No Visual Basic, lembre-se de usar o **definir** palavra-chave ao definir o **ActiveConnection** propriedade a um **Conexão** objeto. Se você omitir a **definir** palavra-chave, você realmente definirá a **ActiveConnection** propriedade igual ao **Conexão** propriedade padrão do objeto  **ConnectionString**. O código funcionará; No entanto, você criará uma conexão adicional para a fonte de dados, que pode ter implicações de desempenho negativo.  
  
 Ao usar o provedor de dados MSOLAP, defina a fonte de dados em uma cadeia de conexão para um nome de servidor e defina o catálogo inicial para o nome de um catálogo da fonte de dados. Para se conectar a um arquivo de cubo que está desconectado de um servidor, defina o local para o caminho completo para o. Arquivos CUB. Em ambos os casos, defina o provedor para o nome do provedor. Por exemplo, a cadeia de caracteres a seguir usa o provedor MSOLAP para conectar-se a um catálogo chamado Bobs vídeo Store em um servidor chamado **Servername**:  
  
```  
"Data Source=Servername;Initial Catalog=Bobs Video Store;Provider=msolap"  
```  
  
 A cadeia de caracteres a seguir se conecta a um arquivo de cubo local no local C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub:  
  
```  
"Location=C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub;Provider=msolap"  
```  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Catalog (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de conjunto de células (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Método Open (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
