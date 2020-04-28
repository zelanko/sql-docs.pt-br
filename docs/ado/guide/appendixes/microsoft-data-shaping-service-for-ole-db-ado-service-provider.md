---
title: Serviço de modelagem de dados da Microsoft para OLE DB (provedor de serviços ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping service for OLE DB
- data shaping service for OLE DB [ADO]
ms.assetid: 523009ce-e01b-4e2d-a7df-816d7688aff0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ddef2feab633627c9549b73787faa1d104d69c5e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926816"
---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>Visão geral do Microsoft Data Shaping Service para OLE DB
> [!IMPORTANT]
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, os aplicativos devem usar XML.

 O serviço de modelagem de dados da Microsoft para o provedor de serviços OLE DB oferece suporte à construção de objetos [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) hierárquicos (moldados) de um provedor de dados.

## <a name="provider-keyword"></a>Palavra-chave Provider
 Para invocar o data Shaping Service para OLE DB, especifique a palavra-chave e o valor a seguir na cadeia de conexão.

```vb
"Provider=MSDataShape"
```

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 Quando esse provedor de serviços é invocado, as propriedades dinâmicas a seguir são adicionadas à coleção [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) do objeto de[conexão](../../../ado/reference/ado-api/connection-object-ado.md) .

|Nome da propriedade dinâmica|Descrição|
|---------------------------|-----------------|
|**Nomes de remodelação exclusivos**|Indica se os objetos do **conjunto de registros** com valores duplicados para suas propriedades de **nome de reformação** são permitidos. Se essa propriedade dinâmica for **verdadeira** e um novo **conjunto de registros** for criado com o mesmo nome de remodelação especificado pelo usuário como um **conjunto de registros**existente, o novo nome de remodelação do objeto **Recordset** será modificado para torná-lo exclusivo. Se essa propriedade for **false** e um novo **conjunto de registros** for criado com o mesmo nome de remodelação especificado pelo usuário que o **conjunto de registros**existente, ambos os objetos **Recordset** terão o mesmo nome de nova forma. Portanto, nenhum **conjunto de registros** pode ser remodelado desde que ambos os conjuntos de registros existam.<br /><br /> O valor padrão da propriedade é **false**.|
|**Provedor de Dados**|Indica o nome do provedor que fornecerá linhas a serem moldadas. Esse valor pode ser nenhum se um provedor não for usado para fornecer linhas.|

 Você também pode definir propriedades dinâmicas graváveis especificando seus nomes como palavras-chave na cadeia de conexão. Por exemplo, no Microsoft Visual Basic, defina a propriedade dinâmica **provedor de dados** como "MSDASQL" especificando:

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MSDataShape;Data Provider=MSDASQL"
```

 Você também pode definir ou recuperar uma propriedade dinâmica especificando seu nome como o índice para a propriedade [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) . Por exemplo, o exemplo de código a seguir obtém e imprime o valor atual da propriedade dinâmica **provedor de dados** e, em seguida, define um novo valor, se CN. DataProvider foi definido como "MSDataShape" (direta ou indiretamente por meio da cadeia de conexão) e a conexão não foi aberta:

```vb
Debug.Print cn.Properties("Data Provider")
cn.Properties("Data Provider") = "MSDASQL"
```

> [!NOTE]
>  A propriedade dinâmica, **provedor de dados**, pode ser definida somente em um objeto de **conexão** não aberto. Depois que a conexão é aberta, a propriedade **provedor de dados** torna-se somente leitura.

 Para obter mais informações sobre o formato de dados, consulte [Data Shaping](../../../ado/guide/data/data-shaping-overview.md).

## <a name="see-also"></a>Consulte Também
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
