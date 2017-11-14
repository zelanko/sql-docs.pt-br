---
title: Registrar o objeto (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Record
helpviewer_keywords:
- Record object [ADO]
ms.assetid: db83ed2c-a8e3-460c-8682-64667e4d5d01
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 26840ff89f61bc3c37cee2fd88c1f53e393528bf
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="record-object-ado"></a>Objeto de registro (ADO)
Representa uma linha de um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) ou o provedor de dados ou um objeto retornado por um provedor de dados estruturados, como um arquivo ou diretório.  
  
## <a name="remarks"></a>Comentários  
 Um **registro** objeto representa uma linha de dados e tem algumas semelhanças conceituais com uma linha **registros**. Dependendo dos recursos do seu provedor, **registro** objetos podem ser retornados diretamente do seu provedor, em vez de uma linha **registros**, por exemplo, quando uma consulta SQL que seleciona apenas uma linha está executado. Ou, um **registro** objeto pode ser obtido diretamente de um **registros** objeto. Ou, um **registro** pode ser retornado diretamente de um provedor de dados estruturados, como o Microsoft Exchange provedor OLE DB.  
  
 Você pode exibir os campos associados a **registro** objeto por meio do [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção no **registro** objeto. ADO permite que colunas com valor de objeto, incluindo **registros**, **SafeArray**e valores escalares no **campos** coleção de **registro** objetos.  
  
 Se o **registro** objeto representa uma linha em uma **registros**, é possível retornar original para que **registros** com o [fonte](../../../ado/reference/ado-api/source-property-ado-record.md) propriedade.  
  
 O **registro** objeto também pode ser usado por provedores de dados estruturados, como o [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)para namespaces estruturados em árvore de modelo. Cada nó na árvore é um **registro** objeto com colunas associadas. As colunas podem representar os atributos de nó e outras informações relevantes. O **registro** objeto pode representar um nó folha e um nó de não-folha na estrutura de árvore. Nós não folha têm outros nós como seu conteúdo, mas nós folha não têm esse conteúdo. Os nós folha normalmente contêm fluxos binários de dados e nós não folha também podem ter um fluxo binário padrão associado a eles. Propriedades de **registro** objeto identificar o tipo de nó.  
  
 O **registro** objeto também representa um modo alternativo para navegar hierarquicamente organizados dados. Um **registro** objeto pode ser criado para representar a raiz de uma subárvore específica em uma estrutura de árvore grande e novos **registro** objetos podem ser abertos para representar nós filho.  
  
 Um recurso (por exemplo, um arquivo ou diretório) pode ser identificado exclusivamente por uma URL absoluta. Um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto é implicitamente criado e definido como o **registro** objeto quando o **registro** é aberto usando uma URL absoluta. Um **Conexão** objeto pode ser definido explicitamente como o **registro** objeto por meio de [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade. Os arquivos e diretórios que podem ser acessados usando o **Conexão** objeto definem o *contexto* no qual **registro** operações podem ocorrer.  
  
 Métodos de navegação e modificação de dados no **registro** objeto também aceita uma URL relativa, que localiza um recurso usando uma URL absoluta ou **Conexão** contexto de objeto como um ponto de partida.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [Absolute e URLs relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 Um **Conexão** objeto está associado a cada **registro** objeto. Portanto, **registro** operações de objeto podem ser parte de uma transação chamando **Conexão** métodos de transação do objeto.  
  
 O **registro** objeto não dá suporte a eventos de ADO e, portanto, não responder a notificações.  
  
 Com os métodos e propriedades de um **registro** do objeto, você pode fazer o seguinte:  
  
-   Definir ou retornar associado **Conexão** do objeto com o [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade.  
  
-   Indicar as permissões de acesso com o [modo](../../../ado/reference/ado-api/mode-property-ado.md) propriedade.  
  
-   Retorna a URL do diretório, se houver, que contém o recurso representado pelo **registro** com o [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) propriedade.  
  
-   Indicar a URL absoluta, uma URL relativa, ou **registros** do qual o **registro** é derivado com a [fonte](../../../ado/reference/ado-api/source-property-ado-record.md) propriedade.  
  
-   Indica o status atual do **registro** com o [estado](../../../ado/reference/ado-api/state-property-ado.md) propriedade.  
  
-   Indique o tipo de **registro** — *simples*, *coleção*, ou *documento estruturado* — com o [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)propriedade.  
  
-   Interromper a execução de uma operação assíncrona com o [Cancelar](../../../ado/reference/ado-api/cancel-method-ado.md) método.  
  
-   Desassociar o **registro** de uma fonte de dados com o [fechar](../../../ado/reference/ado-api/close-method-ado.md) método.  
  
-   Copie o arquivo ou diretório representado por um **registro** para outro local com o [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md) método.  
  
-   Excluir o arquivo ou diretório e subdiretórios, representados por um **registro** com o [ExcluirRegistro](../../../ado/reference/ado-api/deleterecord-method-ado.md) método.  
  
-   Abra um **registros** que contém linhas que representam as subpastas e arquivos da entidade representada pelo **registro** com o [GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md) método.  
  
-   Move (Renomear) o arquivo ou diretório e subdiretórios, representados por um **registro** para outro local com o [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) método.  
  
-   Associar o **registro** com dados existentes de origem ou criar um novo arquivo ou diretório com o [abrir](../../../ado/reference/ado-api/open-method-ado-record.md) método.  
  
 O **registro** objeto é seguro para script.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto Record](../../../ado/reference/ado-api/record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Coleção de campos (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Coleção de propriedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Registros e fluxos](../../../ado/guide/data/records-and-streams.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

