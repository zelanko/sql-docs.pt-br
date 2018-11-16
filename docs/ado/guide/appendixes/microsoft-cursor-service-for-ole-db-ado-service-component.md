---
title: Microsoft Cursor Service para OLE DB (ADO componente de serviço) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], cursor service for OLE DB
- cursor service for OLE DB [ADO]
ms.assetid: 420d0989-7cfb-4c66-a7b5-f4199d13165d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 500a3e38599b0041b036eb148f837afc67260849
ms.sourcegitcommit: 96b2355d54dfad259826e88bdff91cc9344e16f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51350500"
---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>Microsoft Cursor Service para visão geral do OLE DB
O Microsoft Cursor Service para OLE DB complementa as funções de suporte de cursor de provedores de dados. Como resultado, o usuário percebe a funcionalidade relativamente uniforme de todos os provedores de dados.

 O serviço de Cursor disponibiliza as propriedades dinâmicas e aprimora o comportamento de determinados métodos. Por exemplo, o [otimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) propriedade dinâmica permite a criação de índices temporários para facilitar a determinadas operações, como o [localizar](../../../ado/reference/ado-api/find-method-ado.md) método.

 O serviço de Cursor habilita o suporte para atualização em lote em todos os casos. Ele também simula o mais compatível com tipos de cursor, como cursores dinâmicos, quando um provedor de dados pode fornecer apenas cursores com menor capacidade, como os cursores estáticos.

## <a name="keyword"></a>Palavra-chave
 Para invocar esse componente de serviço, defina as [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) ou [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) do objeto [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade **adUseClient**.

```vb
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 Quando o Cursor Service para OLE DB é chamado, as seguintes propriedades dinâmicas são adicionadas para o **conjunto de registros** do objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção. A lista completa das **Conexão** e **conjunto de registros** propriedades dinâmicas do objeto é listado na [índice de propriedade dinâmica do ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md). Os nomes de propriedade associados do OLE DB, quando apropriado, serão incluídos em parênteses após o nome da propriedade ADO.

 Alterações em algumas propriedades dinâmicas não são visíveis à fonte de dados subjacentes depois que o serviço de Cursor foi invocado. Por exemplo, definindo a *tempo limite do comando* propriedade em um **conjunto de registros** não estarão visíveis para o provedor de dados subjacente.

```vb

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 Se seu aplicativo requer que o serviço de Cursor, mas você precisa definir as propriedades dinâmicas no provedor subjacente, defina as propriedades antes de invocar o serviço de Cursor. Configurações de propriedade do objeto de comando sempre são passadas para o provedor de dados subjacente, independentemente do local do cursor. Portanto, você também pode usar um objeto de comando para definir as propriedades a qualquer momento.

> [!NOTE]
>  Não há suporte para a propriedade dinâmica DBPROP_SERVERDATAONINSERT pelo serviço de cursor, mesmo se for suportado pelo provedor de dados subjacente.

|Nome da propriedade|Description|
|-------------------|-----------------|
|Recálculo automático (DBPROP_ADC_AUTORECALC)|Para conjuntos de registros criados com o Data Shaping Service, esse valor indica a frequência com que as colunas calculadas e de agregação são calculadas. O padrão (valor = 1) é recalcular sempre que o Data Shaping Service determina que os valores foram alterados. Se o valor for 0, as colunas calculadas ou de agregação só são calculadas quando a hierarquia é inicialmente criada.|
|Tamanho do lote (DBPROP_ADC_BATCHSIZE)|Indica o número de instruções de atualização que podem ser enviadas em lote antes de serem enviados ao armazenamento de dados. As instruções mais em um lote, as menos viagens de ida e aos dados armazenar.|
|Linhas filho de cache (DBPROP_ADC_CACHECHILDROWS)|Para conjuntos de registros criados com o Data Shaping Service, esse valor indica se o conjunto de registros filho é armazenados em um cache para uso posterior.|
|Versão do mecanismo de cursor (DBPROP_ADC_CEVER)|Indica a versão do serviço de Cursor que está sendo usado.|
|Manter o Status de alteração (DBPROP_ADC_MAINTAINCHANGESTATUS)|Indica o texto do comando usado para sincronizar novamente a uma ou mais linhas em uma junção de várias tabelas.|
|[Otimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|Indica se um índice deve ser criado. Quando definido como **verdadeira**, autoriza a criação temporária de índices para melhorar a execução de determinadas operações.|
|[Alterar a forma de nome](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|Indica o nome da **conjunto de registros**. Pode ser referenciado dentro do atual ou a subsequente, comandos de formatação de dados.|
|[Comando de ressincronização](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|Indica uma cadeia de caracteres de comando personalizado que é usada pelas [ressincronizar](../../../ado/reference/ado-api/resync-method.md) método quando o [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) propriedade está em vigor.|
|[Catálogo exclusivo](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica o nome do banco de dados que contém a tabela referenciada na **tabela exclusiva** propriedade.|
|[Esquema exclusivo](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica o nome do proprietário da tabela referenciada na **tabela exclusiva** propriedade.|
|[Tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica o nome de uma tabela em uma **Recordset** criado a partir de várias tabelas que podem ser modificadas pelo inserções, atualizações ou exclusões.|
|Critérios de atualização (DBPROP_ADC_UPDATECRITERIA)|Indica quais campos na **onde** cláusula são usados para lidar com conflitos que ocorrem durante uma atualização.|
|[Atualizar a ressincronização](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) (DBPROP_ADC_UPDATERESYNC)|Indica se o **ressincronizar** método implicitamente é invocado após o [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método (e seu comportamento), quando o **tabela exclusiva** propriedade está em vigor.|

 Você também pode definir ou recuperar uma propriedade dinâmica especificando seu nome como o índice para o **propriedades** coleção. Por exemplo, obter e imprimir o valor atual do [otimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) propriedades dinâmicas, em seguida, defina um novo valor, da seguinte maneira:

```vb
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>Comportamento de propriedade interna
 O Cursor Service para OLE DB também afeta o comportamento de determinadas propriedades internas.

|Nome da propriedade|Description|
|-------------------|-----------------|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|Complementa os tipos de cursores que estão disponíveis para um **conjunto de registros**.|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|Complementa os tipos de bloqueios disponíveis para um **conjunto de registros**. Permite o atualizações em lotes.|
|[Sort](../../../ado/reference/ado-api/sort-property.md)|Especifica o campo de um ou mais nomes que o **Recordset** é classificada e se cada campo é classificado em ordem crescente ou decrescente.|

## <a name="method-behavior"></a>Comportamento do método
 O Cursor Service para OLE DB habilita ou afeta o comportamento do [campo](../../../ado/reference/ado-api/field-object.md) do objeto [Append](../../../ado/reference/ado-api/append-method-ado.md) método; e o **conjunto de registros** do objeto [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md), [Ressincronizar](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), e [salvar](../../../ado/reference/ado-api/save-method.md) métodos.
