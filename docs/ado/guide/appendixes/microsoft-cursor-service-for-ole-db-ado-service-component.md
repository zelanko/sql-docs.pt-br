---
title: Serviço de cursor da Microsoft para OLE DB (componente de serviço ADO) | Microsoft Docs
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
ms.openlocfilehash: e7e5b9a973e5ccf04f92a2162d88ee25b7fa5242
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926793"
---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>Visão geral do serviço de cursor da Microsoft para OLE DB
O serviço de cursor da Microsoft para OLE DB complementa as funções de suporte de cursor dos provedores de dados. Como resultado, o usuário percebe uma funcionalidade relativamente uniforme de todos os provedores de dados.

 O serviço de cursor torna as propriedades dinâmicas disponíveis e aprimora o comportamento de determinados métodos. Por exemplo, a propriedade [otimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) dinâmico permite a criação de índices temporários para facilitar determinadas operações, como o método [Find](../../../ado/reference/ado-api/find-method-ado.md) .

 O serviço de cursor habilita o suporte para atualização em lotes em todos os casos. Ele também simula tipos de cursor mais capacitados, como cursores dinâmicos, quando um provedor de dados só pode fornecer cursores menos capacitados, como cursores estáticos.

## <a name="keyword"></a>Palavra-chave
 Para invocar esse componente de serviço, defina a propriedade [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) do [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) ou do objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) como **adUseClient**.

```vb
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 Quando o serviço de cursor para OLE DB é invocado, as propriedades dinâmicas a seguir são adicionadas à coleção de [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) do objeto **Recordset** . A lista completa de propriedades dinâmicas de **conexão** e objeto **Recordset** está listada no [índice de propriedades dinâmicas do ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md). Os nomes de propriedade OLE DB associados, quando apropriado, são incluídos entre parênteses após o nome da propriedade ADO.

 As alterações em algumas propriedades dinâmicas não são visíveis para a fonte de dados subjacente depois que o serviço de cursor é invocado. Por exemplo, definir a propriedade de *tempo limite do comando* em um **conjunto de registros** não será visível para o provedor de dados subjacente.

```vb

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 Se seu aplicativo requer o serviço de cursor, mas você precisa definir propriedades dinâmicas no provedor subjacente, defina as propriedades antes de invocar o serviço de cursor. As configurações de propriedade de objeto de comando sempre são passadas para o provedor de dados subjacente, independentemente do local do cursor. Portanto, você também pode usar um objeto de comando para definir as propriedades a qualquer momento.

> [!NOTE]
>  Não há suporte para a propriedade dinâmica DBPROP_SERVERDATAONINSERT pelo serviço de cursor, mesmo que ele tenha suporte do provedor de dados subjacente.

|Nome da propriedade|DESCRIÇÃO|
|-------------------|-----------------|
|Recálculo automático (DBPROP_ADC_AUTORECALC)|Para conjuntos de registros criados com o data Shaping Service, esse valor indica a frequência com que as colunas calculadas e agregadas são calculadas. O padrão (valor = 1) é recalcular sempre que o serviço de data Shaping determinar que os valores foram alterados. Se o valor for 0, as colunas calculadas ou agregadas só serão calculadas quando a hierarquia for inicialmente compilada.|
|Tamanho do lote (DBPROP_ADC_BATCHSIZE)|Indica o número de instruções UPDATE que podem ser agrupadas em lote antes de serem enviadas ao armazenamento de dados. Quanto mais instruções em um lote, menos viagens de ida e volta para o armazenamento de dados.|
|Linhas filhas de cache (DBPROP_ADC_CACHECHILDROWS)|Para conjuntos de registros criados com o data Shaping Service, esse valor indica se os conjuntos de registros filho são armazenados em um cache para uso posterior.|
|Versão do mecanismo de cursor (DBPROP_ADC_CEVER)|Indica a versão do serviço de cursor que está sendo usado.|
|Manter status de alteração (DBPROP_ADC_MAINTAINCHANGESTATUS)|Indica o texto do comando usado para a ressincronização de uma ou mais linhas em uma junção de várias tabelas.|
|[Formato](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|Indica se um índice deve ser criado. Quando definido como **true**, o autoriza a criação temporária de índices para melhorar a execução de determinadas operações.|
|[Remodelar nome](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|Indica o nome do **conjunto de registros**. Podem ser referenciados nos comandos de data Shaping atuais, ou subsequentes.|
|[Comando Ressync](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|Indica uma cadeia de caracteres de comando Personalizada que é usada pelo método de [ressincronização](../../../ado/reference/ado-api/resync-method.md) quando a propriedade de [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) está em vigor.|
|[Catálogo exclusivo](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica o nome do banco de dados que contém a tabela referenciada na propriedade de **tabela exclusiva** .|
|[Esquema exclusivo](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica o nome do proprietário da tabela referenciada na propriedade de **tabela exclusiva** .|
|[Tabela única](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica o nome de uma tabela em um **conjunto de registros** criado a partir de várias tabelas que podem ser modificadas por inserções, atualizações ou exclusões.|
|Critérios de atualização (DBPROP_ADC_UPDATECRITERIA)|Indica quais campos na cláusula **Where** são usados para lidar com colisões que ocorrem durante uma atualização.|
|[Atualizar ressincronização](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) (DBPROP_ADC_UPDATERESYNC)|Indica se o método de **ressincronização** é invocado implicitamente após o método [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) (e seu comportamento) quando a propriedade de **tabela exclusiva** está em vigor.|

 Você também pode definir ou recuperar uma propriedade dinâmica especificando seu nome como o índice para a coleção de **Propriedades** . Por exemplo, obtenha e imprima o valor atual da propriedade [otimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) dinâmico e, em seguida, defina um novo valor, da seguinte maneira:

```vb
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>Comportamento de propriedade interna
 O serviço de cursor para OLE DB também afeta o comportamento de determinadas propriedades internas.

|Nome da propriedade|DESCRIÇÃO|
|-------------------|-----------------|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|Complementa os tipos de cursores que estão disponíveis para um **conjunto de registros**.|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|Complementa os tipos de bloqueios disponíveis para um **conjunto de registros**. Habilita atualizações em lotes.|
|[Classificar](../../../ado/reference/ado-api/sort-property.md)|Especifica um ou mais nomes de campos nos quais o **conjunto de registros** é classificado e se cada campo é classificado em ordem crescente ou decrescente.|

## <a name="method-behavior"></a>Comportamento do método
 O serviço de cursor para OLE DB habilita ou afeta o comportamento do método [Append](../../../ado/reference/ado-api/append-method-ado.md) do objeto [Field](../../../ado/reference/ado-api/field-object.md) ; e os métodos [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md), [Ressync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)e [Save](../../../ado/reference/ado-api/save-method.md) do objeto **Recordset** .
