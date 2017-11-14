---
title: "Serviço Microsoft Cursor para OLE DB (componente do serviço de ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], cursor service for OLE DB
- cursor service for OLE DB [ADO]
ms.assetid: 420d0989-7cfb-4c66-a7b5-f4199d13165d
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d7a1f8568b633417196c6c9dda3e8a3615146603
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>Serviço de Cursor da Microsoft para visão geral do OLE DB
O serviço de Cursor da Microsoft para OLE DB complementa as funções de suporte de cursor de provedores de dados. Como resultado, o usuário percebe funcionalidade relativamente uniforme de todos os provedores de dados.

 O serviço de Cursor disponibiliza propriedades dinâmicas e aprimora o comportamento de certos métodos. Por exemplo, o [otimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) propriedade dinâmica permite a criação de índices temporários para facilitar a determinadas operações, como o [localizar](../../../ado/reference/ado-api/find-method-ado.md) método.

 O serviço de Cursor habilita o suporte para atualização em lotes em todos os casos. Ele também simula mais compatíveis com tipos de cursor, como cursores dinâmicos, quando um provedor de dados pode fornecer apenas cursores menor capacidade, como Cursores estáticos.

## <a name="keyword"></a>Palavra-chave
 Para invocar esse componente de serviço, defina o [registros](../../../ado/reference/ado-api/recordset-object-ado.md) ou [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) do objeto [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade **adUseClient**.

```
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 Quando o serviço de Cursor do OLE DB é chamado, as propriedades dinâmicas a seguir são adicionadas para o **registros** do objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção. A lista completa de **Conexão** e **registros** propriedades dinâmicas do objeto está listado no [índice de propriedade dinâmica de ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md). Os nomes de propriedade OLE DB associados, quando apropriado, são incluídos entre parênteses após o nome da propriedade ADO.

 Alterações em algumas propriedades dinâmicas não são visíveis para a fonte de dados depois que o serviço de Cursor foi invocado. Por exemplo, se você definir o *tempo limite do comando* propriedade em uma **Recordset** não ficarão visíveis para o provedor de dados subjacente.

```

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 Se seu aplicativo requer que o serviço de Cursor, mas você precisa definir as propriedades dinâmicas no provedor subjacente, defina as propriedades antes de chamar o serviço de Cursor. Configurações de propriedade do objeto de comando sempre são passadas para o provedor de dados subjacente, independentemente do local do cursor. Portanto, você também pode usar um objeto de comando para definir as propriedades a qualquer momento.

> [!NOTE]
>  Não há suporte para a propriedade dinâmica DBPROP_SERVERDATAONINSERT pelo serviço de cursor, mesmo se houver suporte pelo provedor de dados subjacente.

|Nome da propriedade|Description|
|-------------------|-----------------|
|Recálculo automático (DBPROP_ADC_AUTORECALC)|Para conjuntos de registros criados com o Data Shaping Service, esse valor indica a frequência colunas calculadas e de agregação são calculadas. O padrão (valor = 1) é recalcular sempre que o Data Shaping Service determina que os valores foram alterados. Se o valor for 0, as colunas calculadas ou agregação só são calculadas quando a hierarquia é criada inicialmente.|
|Tamanho do lote (DBPROP_ADC_BATCHSIZE)|Indica o número de instruções de atualização que pode ser colocado em lote antes de serem enviados para o repositório de dados. As instruções mais em um lote, as menos viagens de ida e aos dados de repositório.|
|Linhas filho de cache (DBPROP_ADC_CACHECHILDROWS)|Para conjuntos de registros criados com o Data Shaping Service, esse valor indica se o conjunto de registros filho é armazenados em um cache para uso posterior.|
|Versão do mecanismo de cursor (DBPROP_ADC_CEVER)|Indica a versão do serviço de Cursor que está sendo usado.|
|Manter o Status de alteração (DBPROP_ADC_MAINTAINCHANGESTATUS)|Indica o texto do comando usado para ressincronizar uma ou mais linhas em uma junção de várias tabelas.|
|[Otimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|Indica se um índice deve ser criado. Quando definido como **True**, autoriza a criação temporária de índices para melhorar a execução de determinadas operações.|
|[Alterar a forma de nome](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|Indica o nome do **registros**. Pode ser referenciado em atual ou a subsequente, comandos de formatação de dados.|
|[Sincronizar de comando](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|Indica uma cadeia de caracteres de comando personalizado que é usada pelo [Resync](../../../ado/reference/ado-api/resync-method.md) método quando o [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) propriedade está em vigor.|
|[Catálogo exclusivo](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica o nome do banco de dados que contém a tabela referenciada no **tabela exclusiva** propriedade.|
|[Esquema exclusivo](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica o nome do proprietário da tabela referenciada no **tabela exclusiva** propriedade.|
|[Tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica o nome de uma tabela em uma **registros** criado a partir de várias tabelas que podem ser modificadas por inserções, atualizações ou exclusões.|
|Critérios de atualização (DBPROP_ADC_UPDATECRITERIA)|Indica quais campos o **onde** cláusula são usados para controlar conflitos que ocorrem durante uma atualização.|
|[Atualizar ressincronização](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) (DBPROP_ADC_UPDATERESYNC)|Indica se o **Resync** método é chamado implicitamente após o [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método (e seu comportamento), quando o **tabela exclusiva** propriedade está em vigor.|

 Você também pode definir ou recuperar uma propriedade dinâmica especificando seu nome como o índice para o **propriedades** coleção. Por exemplo, obter e imprimir o valor atual de [otimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) propriedades dinâmicas, em seguida, defina um novo valor, da seguinte maneira:

```
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>Comportamento de propriedade interna
 O serviço de Cursor do OLE DB também afeta o comportamento de determinadas propriedades internas.

|Nome da propriedade|Description|
|-------------------|-----------------|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|Complementa os tipos de cursores que estão disponíveis para um **registros**.|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|Complementa os tipos de bloqueios disponíveis para um **registros**. Permite o atualizações em lotes.|
|[Sort](../../../ado/reference/ado-api/sort-property.md)|Especifica o campo de um ou mais nomes que o **Recordset** é classificado e se cada campo é classificado em ordem crescente ou decrescente.|

## <a name="method-behavior"></a>Comportamento do método
 O serviço de Cursor do OLE DB permite ou afeta o comportamento do [campo](../../../ado/reference/ado-api/field-object.md) do objeto [Append](../../../ado/reference/ado-api/append-method-ado.md) método; e o **registros** do objeto [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md), [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), e [salvar](../../../ado/reference/ado-api/save-method.md) métodos.

