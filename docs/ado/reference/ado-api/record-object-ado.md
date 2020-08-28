---
description: Objeto Record (ADO)
title: Objeto de registro (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6066d43bfa52d65ee133fd748f76fc651fac7379
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989857"
---
# <a name="record-object-ado"></a>Objeto Record (ADO)
Representa uma linha de um [conjunto de registros](./recordset-object-ado.md) ou do provedor de dados, ou um objeto retornado por um provedor de dados semiestruturado, como um arquivo ou diretório.  
  
## <a name="remarks"></a>Comentários  
 Um objeto de **registro** representa uma linha de dados e tem algumas semelhanças conceituais com um conjunto de **registros**de uma linha. Dependendo dos recursos do seu provedor, os objetos de **registro** podem ser retornados diretamente do seu provedor em vez de um conjunto de **registros**de uma linha, por exemplo, quando uma consulta SQL que seleciona apenas uma linha é executada. Ou, um objeto de **registro** pode ser obtido diretamente de um objeto **Recordset** . Ou, um **registro** pode ser retornado diretamente de um provedor para dados semiestruturados, como o provedor de OLE DB do Microsoft Exchange.  
  
 Você pode exibir os campos associados ao objeto **Record** por meio da coleção [Fields](./fields-collection-ado.md) no objeto **Record** . O ADO permite colunas com valor de objeto, incluindo **conjuntos de registros**, **SafeArray**e valores escalares na coleção **Fields** de objetos **Record** .  
  
 Se o objeto de **registro** representar uma linha em um **conjunto de registros**, será possível retornar a esse **conjunto de registros** original com a propriedade [Source](./source-property-ado-record.md) .  
  
 O objeto **Record** também pode ser usado por provedores de dados semiestruturados, como o [provedor de OLE DB da Microsoft para publicação na Internet](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md), para modelar namespaces estruturados em árvore. Cada nó na árvore é um objeto de **registro** com colunas associadas. As colunas podem representar os atributos desse nó e outras informações relevantes. O objeto **Record** pode representar um nó folha e um nó não folha na estrutura de árvore. Nós não folha têm outros nós como seu conteúdo, mas nós folha não têm esse conteúdo. Os nós folha normalmente contêm fluxos binários de dados e nós não folha também podem ter um fluxo binário padrão associado a eles. As propriedades no objeto de **registro** identificam o tipo de nó.  
  
 O objeto **Record** também representa uma maneira alternativa para navegar em dados hierarquicamente organizados. Um objeto de **registro** pode ser criado para representar a raiz de uma subárvore específica em uma estrutura de árvore grande e novos objetos de **registro** podem ser abertos para representar nós filho.  
  
 Um recurso (por exemplo, um arquivo ou diretório) pode ser identificado exclusivamente por uma URL absoluta. Um objeto de [conexão](./connection-object-ado.md) é criado implicitamente e definido como o objeto **Record** quando o **registro** é aberto usando uma URL absoluta. Um objeto de **conexão** pode ser explicitamente definido para o objeto **Record** por meio da propriedade [ActiveConnection](./activeconnection-property-ado.md) . Os arquivos e diretórios que podem ser acessados usando o objeto de **conexão** definem o *contexto* no qual podem ocorrer operações de **registro** .  
  
 Os métodos de navegação e modificação de dados no objeto de **registro** também aceitam uma URL relativa, que localiza um recurso usando uma URL absoluta ou o contexto do objeto de **conexão** como um ponto de partida.  
  
> [!NOTE]
>  As URLs que usam o esquema http invocarão automaticamente o [provedor do Microsoft OLE DB para publicação na Internet](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [URLs absolutas e relativas](../../guide/data/absolute-and-relative-urls.md).  
  
 Um objeto de **conexão** é associado a cada objeto de **registro** . Portanto, as operações de objeto de **registro** podem fazer parte de uma transação invocando métodos de transação de objeto de **conexão** .  
  
 O objeto **Record** não oferece suporte a eventos ADO e, portanto, não responderá às notificações.  
  
 Com os métodos e as propriedades de um objeto de **registro** , você pode fazer o seguinte:  
  
-   Defina ou retorne o objeto de **conexão** associado com a propriedade [ActiveConnection](./activeconnection-property-ado.md) .  
  
-   Indique as permissões de acesso com a propriedade [Mode](./mode-property-ado.md) .  
  
-   Retorne a URL do diretório, se houver, que contém o recurso representado pelo **registro** com a propriedade [ParentURL](./parenturl-property-ado.md) .  
  
-   Indique a URL absoluta, a URL relativa ou o **conjunto de registros** do qual o **registro** é derivado com a propriedade [Source](./source-property-ado-record.md) .  
  
-   Indique o status atual do **registro** com a propriedade [State](./state-property-ado.md) .  
  
-   Indique o tipo de **registro**  -  *simples*, *coleção*ou *documento estruturado* -com a propriedade [RecordType](./recordtype-property-ado.md).  
  
-   Interrompa a execução de uma operação assíncrona com o método [Cancel](./cancel-method-ado.md) .  
  
-   Desassocie o **registro** de uma fonte de dados com o método [Close](./close-method-ado.md) .  
  
-   Copie o arquivo ou diretório representado por um **registro** para outro local com o método [CopyRecord](./copyrecord-method-ado.md) .  
  
-   Exclua o arquivo, o diretório e os subdiretórios, representados por um **registro** com o método [DeleteRecord](./deleterecord-method-ado.md) .  
  
-   Abra um **conjunto de registros** que contenha linhas que representem os subdiretórios e arquivos da entidade representada pelo **registro** com o método [GetChildren](./getchildren-method-ado.md) .  
  
-   Mova (renomeie) o arquivo, o diretório e os subdiretórios, representados por um **registro** para outro local com o método [MoveRecord](./moverecord-method-ado.md) .  
  
-   Associe o **registro** a uma fonte de dados existente ou crie um novo arquivo ou diretório com o método [Open](./open-method-ado-record.md) .  
  
 O objeto de **registro** é seguro para scripts.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto Record](./record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Coleção Fields (ADO)](./fields-collection-ado.md)   
 [Coleção Properties (ADO)](./properties-collection-ado.md)   
 [Registros e fluxos](../../guide/data/records-and-streams.md)   
 [Objeto Recordset (ADO)](./recordset-object-ado.md)