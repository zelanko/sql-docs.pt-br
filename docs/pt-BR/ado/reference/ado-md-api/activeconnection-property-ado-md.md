---
title: Propriedade ActiveConnection (ADO MD) | Microsoft Docs
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
- ActiveConnection
- Cellset::ActiveConnection
- Catalog::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO MD]
ms.assetid: 2509b32c-a995-4364-9152-d8c83129bdd8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 708f33d5cf4881040bef714ce62d9082ecc6528f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="activeconnection-property-ado-md"></a>Propriedade ActiveConnection (ADO MD)
Indica para qual ADO [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) o conjunto de células atual do objeto ou o catálogo ao qual pertence atualmente.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **Variant** que contém uma cadeia de caracteres que define uma conexão ou **Conexão** objeto. O padrão é vazio.  
  
## <a name="remarks"></a>Remarks  
 Você pode definir essa propriedade para um ADO válido **Conexão** objeto ou uma cadeia de caracteres de conexão válido. Quando essa propriedade é definida como uma cadeia de caracteres de conexão, o provedor cria um novo **Conexão** usando esta definição de objeto e abre a conexão.  
  
 Se você usar o *ActiveConnection* argumento do [abrir](../../../ado/reference/ado-md-api/open-method-ado-md.md) método para abrir um [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto, o **ActiveConnection** será de propriedade herde o valor do argumento.  
  
 Definindo o **ActiveConnection** propriedade de um [catálogo](../../../ado/reference/ado-md-api/catalog-object-ado-md.md) do objeto para **nada** libera os dados associados, inclusive dados no [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) coleta e qualquer relacionadas [dimensão](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [hierarquia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md), e [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objetos. Fechando uma **Conexão** objeto que foi usado para abrir um **catálogo** tem o mesmo efeito que definir a **ActiveConnection** propriedade **nada**.  
  
 Alterando o banco de dados padrão da conexão referenciada pelo **ActiveConnection** propriedade de um **catálogo** objeto invalida o conteúdo do **catálogo**.  
  
 Um erro ocorrerá se você tentar alterar o **ActiveConnection** propriedade um abra **conjunto de células** objeto.  
  
> [!NOTE]
>  No Visual Basic, lembre-se de usar o **definir** palavra-chave ao definir o **ActiveConnection** propriedade para um **Conexão** objeto. Se você omitir o **definir** palavra-chave, você realmente definirá o **ActiveConnection** propriedade igual ao **Conexão** propriedade padrão do objeto  **ConnectionString**. O código funcionará; No entanto, você criará uma conexão adicional para a fonte de dados, que pode ter implicações de desempenho negativo.  
  
 Ao usar o provedor de dados MSOLAP, defina a fonte de dados em uma cadeia de conexão para um nome de servidor e defina o catálogo inicial para o nome de um catálogo da fonte de dados. Para se conectar a um arquivo de cubo que está desconectado de um servidor, defina o local para o caminho completo para o. Arquivos CUB. Em ambos os casos, defina o provedor para o nome do provedor. Por exemplo, a cadeia de caracteres a seguir usa o provedor MSOLAP para conectar-se a um catálogo denominado Bobs repositório de vídeo em um servidor chamado **Servername**:  
  
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
