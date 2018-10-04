---
title: Registrar o objeto (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Record
helpviewer_keywords:
- Record object [ADO]
ms.assetid: db83ed2c-a8e3-460c-8682-64667e4d5d01
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9c3688bcd713eab1fed94efab0a5c88f41b7c529
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47758834"
---
# <a name="record-object-ado"></a>Objeto Record (ADO)
Representa uma linha de uma [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ou o provedor de dados ou um objeto retornado por um provedor de dados semiestruturados, como um arquivo ou diretório.  
  
## <a name="remarks"></a>Comentários  
 Um **registro** objeto representa uma linha de dados e tem algumas semelhanças conceituais com uma linha **conjunto de registros**. Dependendo dos recursos do seu provedor **registro** objetos podem ser retornados diretamente do seu provedor, em vez de uma linha **conjunto de registros**, por exemplo, quando uma consulta SQL que seleciona apenas uma linha é executado. Ou, um **registro** objeto pode ser obtido diretamente de um **Recordset** objeto. Ou, um **registro** podem ser retornados diretamente de um provedor para dados semiestruturados, como o Microsoft Exchange provedor OLE DB.  
  
 Você pode exibir os campos associados a **registro** do objeto por meio das [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleta no **registro** objeto. ADO permite que colunas com valor de objeto, incluindo **conjunto de registros**, **SafeArray**e os valores escalares no **campos** coleção de **registro** objetos.  
  
 Se o **registro** objeto representa uma linha em uma **conjunto de registros**, é possível retornar ao ou original **conjunto de registros** com o [origem](../../../ado/reference/ado-api/source-property-ado-record.md) propriedade.  
  
 O **registro** objeto também pode ser usado por provedores de dados semiestruturados, como o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md), para namespaces estruturados em árvore do modelo. Cada nó na árvore é um **registro** objeto com colunas associadas. As colunas podem representam os atributos do nó e outras informações relevantes. O **registro** objeto pode representar um nó folha e um nó não folha na estrutura de árvore. Nós não folha têm outros nós como seu conteúdo, mas nós folha não têm esse conteúdo. Normalmente, nós folha contêm fluxos binários de dados e nós não folha também podem ter um fluxo binário de padrão associado a eles. Propriedades de **registro** objeto identificar o tipo de nó.  
  
 O **registro** objeto também representa um modo alternativo para navegar hierarquicamente organizados dados. Um **registro** objeto pode ser criado para representar a raiz de uma subárvore específica em uma estrutura de árvore grande e novos **registro** objetos podem ser abertos para representar nós filho.  
  
 Um recurso (por exemplo, um arquivo ou diretório) pode ser identificado exclusivamente por uma URL absoluta. Um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto é implicitamente criado e definido como o **registro** objeto quando o **registro** é aberto usando uma URL absoluta. Um **Conexão** objeto pode ser definido explicitamente como o **registro** por meio do objeto de [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade. Os arquivos e diretórios que podem ser acessados usando o **Conexão** objeto definem o *contexto* em que **registro** operações podem ocorrer.  
  
 Métodos de navegação e modificação de dados na **registro** objeto também aceitam uma URL relativa, que localiza um recurso usando uma URL absoluta ou o **Conexão** contexto de objeto como um ponto de partida.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [absoluta e relativa URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 Um **Conexão** objeto está associado com cada **registro** objeto. Portanto, **registro** operações de objeto podem ser parte de uma transação invocando **Conexão** métodos de transação do objeto.  
  
 O **registro** objeto não oferece suporte a eventos ADO e, portanto, não responderá às notificações.  
  
 Com os métodos e propriedades de um **registro** do objeto, você pode fazer o seguinte:  
  
-   Definir ou retornar associado **Conexão** do objeto com o [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade.  
  
-   Indicar as permissões de acesso com o [modo](../../../ado/reference/ado-api/mode-property-ado.md) propriedade.  
  
-   Retornar a URL do diretório, se houver, que contém o recurso representado pela **registro** com o [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) propriedade.  
  
-   Indique a URL absoluta, a URL relativa, ou **conjunto de registros** da qual o **registro** é derivado com o [origem](../../../ado/reference/ado-api/source-property-ado-record.md) propriedade.  
  
-   Indicar o status atual do **registro** com o [estado](../../../ado/reference/ado-api/state-property-ado.md) propriedade.  
  
-   Indicar o tipo de **registro** — *simples*, *coleção*, ou *documento estruturado* — com o [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)propriedade.  
  
-   Parar a execução de uma operação assíncrona com o [Cancelar](../../../ado/reference/ado-api/cancel-method-ado.md) método.  
  
-   Desassociar a **registro** de uma fonte de dados com o [fechar](../../../ado/reference/ado-api/close-method-ado.md) método.  
  
-   Copie o arquivo ou diretório, representado por um **registro** em outro local com o [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md) método.  
  
-   Excluir o arquivo ou diretório e subdiretórios, representados por um **registro** com o [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md) método.  
  
-   Abra uma **conjunto de registros** que contém linhas que representam os subdiretórios e arquivos da entidade representada pela **registro** com o [GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md) método.  
  
-   Move (Renomear) o arquivo ou diretório e subdiretórios, representados por um **registro** em outro local com o [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) método.  
  
-   Associar o **registro** com os dados existentes de origem, ou crie um novo arquivo ou diretório com o [abrir](../../../ado/reference/ado-api/open-method-ado-record.md) método.  
  
 O **registro** objeto é seguro para script.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto Record](../../../ado/reference/ado-api/record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Coleção de propriedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Registros e fluxos](../../../ado/guide/data/records-and-streams.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
