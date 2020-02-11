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
ms.openlocfilehash: ae0b32385b98ac1b48688a7f89bbd7c91842a106
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67911591"
---
# <a name="activeconnection-property-ado-md"></a>Propriedade ActiveConnection (ADO MD)
Indica a qual objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) ADO o células ou o catálogo atual pertence atualmente.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna uma **variante** que contém uma cadeia de caracteres que define um objeto Connection ou **Connection** . O padrão é vazio.  
  
## <a name="remarks"></a>Comentários  
 Você pode definir essa propriedade como um objeto de **conexão** ADO válido ou uma cadeia de conexão válida. Quando essa propriedade é definida como uma cadeia de conexão, o provedor cria um novo objeto de **conexão** usando essa definição e abre a conexão.  
  
 Se você usar o argumento *ActiveConnection* do método [Open](../../../ado/reference/ado-md-api/open-method-ado-md.md) para abrir um objeto [células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) , a propriedade **ActiveConnection** irá herdar o valor do argumento.  
  
 Definir a **propriedade ActiveConnection** de um objeto de [Catálogo](../../../ado/reference/ado-md-api/catalog-object-ado-md.md) como **Nothing** libera os dados associados, incluindo dados na coleção [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) e quaisquer objetos de [dimensão](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [hierarquia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md)e [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) relacionados. Fechar um objeto de **conexão** que foi usado para abrir um **Catálogo** tem o mesmo efeito que definir a propriedade **ActiveConnection** como **Nothing**.  
  
 A alteração do banco de dados padrão da conexão referenciada pela propriedade **ActiveConnection** de um objeto de **Catálogo** invalida o conteúdo do **Catálogo**.  
  
 Ocorrerá um erro se você tentar alterar a propriedade **ActiveConnection** para um objeto Open **células** .  
  
> [!NOTE]
>  Em Visual Basic, lembre-se de usar a palavra-chave **set** ao definir a propriedade **ActiveConnection** como um objeto **Connection** . Se você omitir a palavra-chave **set** , na verdade estará definindo a propriedade **ActiveConnection** igual à propriedade padrão do objeto de **conexão** , **ConnectionString**. O código funcionará; no entanto, você criará uma conexão adicional com a fonte de dados, que pode ter implicações de desempenho negativas.  
  
 Ao usar o provedor de dados MSOLAP, defina a fonte de dados em uma cadeia de conexão para um nome de servidor e defina o catálogo inicial como o nome de um catálogo da fonte de dados. Para se conectar a um arquivo de cubo que está desconectado de um servidor, defina o local como o caminho completo para o. Arquivo CUB. Em ambos os casos, defina o provedor como o nome do provedor. Por exemplo, a cadeia de caracteres a seguir usa o provedor MSOLAP para se conectar a um **Catálogo chamado bobs**Video Store em um servidor chamado ServerName:  
  
```  
"Data Source=Servername;Initial Catalog=Bobs Video Store;Provider=msolap"  
```  
  
 A cadeia de caracteres a seguir se conecta a um arquivo de cubo local no local C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub:  
  
```  
"Location=C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub;Provider=msolap"  
```  
  
## <a name="applies-to"></a>Aplica-se A  
  
|||  
|-|-|  
|[Objeto Catalog (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de células (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Objeto de conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Método Open (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
