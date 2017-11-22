---
title: "Microsoft Data Shaping Service para OLE DB (provedor de serviços de ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], data shaping service for OLE DB
- data shaping service for OLE DB [ADO]
ms.assetid: 523009ce-e01b-4e2d-a7df-816d7688aff0
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 624bc851727e9d929c4d83721ac64352669cf643
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>Microsoft Data Shaping Service para visão geral do OLE DB
> [!IMPORTANT]
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, os aplicativos devem usar XML.

 O Microsoft Data Shaping Service para o provedor OLE DB oferece suporte a construção de hierárquica (formatado) [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objetos de um provedor de dados.

## <a name="provider-keyword"></a>Palavra-chave do provedor
 Para invocar o Data Shaping Service para OLE DB, especifique a seguinte palavra-chave e valor na cadeia de conexão.

```
"Provider=MSDataShape"
```

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 Quando esse provedor de serviços é chamado, as propriedades dinâmicas a seguir são adicionadas para o [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção do[Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.

|Nome de propriedade dinâmica|Description|
|---------------------------|-----------------|
|**Nomes de reformatação exclusivo**|Indica se **registros** objetos com valores duplicados para seus **nome remodelar** propriedades são permitidas. Se essa propriedade dinâmica é **True** e um novo **registros** é criado com o mesmo nome especificado pelo usuário a reformatação existente **registros**, em seguida, o novo  **Conjunto de registros** reformatação nome de objeto é modificado para torná-lo exclusivo. Se essa propriedade for **False** e um novo **registros** é criado com o mesmo nome especificado pelo usuário a reformatação existente **Recordset**, ambos **conjunto de registros**  objetos terão o mesmo nome de reformatação. Portanto, nenhuma **registros** pode ser reformatado desde que ambos os conjuntos de registros existem.<br /><br /> O valor padrão da propriedade é **False**.|
|**Provedor de dados**|Indica o nome do provedor que fornece linhas a ser formatado. Esse valor pode ser nenhum se não for usado um provedor para fornecer linhas.|

 Você também pode definir propriedades dinâmicas graváveis especificando seus nomes como palavras-chave na cadeia de conexão. Por exemplo, no Microsoft Visual Basic, defina o **provedor de dados** propriedade dinâmica para "MSDASQL" especificando:

```
Dim cn as New ADODB.Connection
cn.Open "Provider=MSDataShape;Data Provider=MSDASQL"
```

 Você também pode definir ou recuperar uma propriedade dinâmica especificando seu nome como o índice para o [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) propriedade. Por exemplo, o exemplo de código a seguir obtém e imprime o valor atual de **provedor de dados** propriedades dinâmicas, em seguida, define um novo valor se cn. DataProvider foi definida como "MSDataShape" (direta ou indiretamente por meio da cadeia de conexão) e a conexão não foi aberta:

```
Debug.Print cn.Properties("Data Provider")
cn.Properties("Data Provider") = "MSDASQL"
```

> [!NOTE]
>  A propriedade dinâmica, **provedor de dados**, pode ser definido apenas em um não aberta **Conexão** objeto. Depois que a conexão for aberta, o **provedor de dados** propriedade será somente leitura.

 Para obter mais informações sobre formatação de dados, consulte [modelagem de dados](../../../ado/guide/data/data-shaping-overview.md).

## <a name="see-also"></a>Consulte também
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
