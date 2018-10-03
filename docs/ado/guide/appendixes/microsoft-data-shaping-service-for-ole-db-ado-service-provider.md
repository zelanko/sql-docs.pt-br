---
title: Microsoft Data Shaping Service para OLE DB (provedor de serviços do ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping service for OLE DB
- data shaping service for OLE DB [ADO]
ms.assetid: 523009ce-e01b-4e2d-a7df-816d7688aff0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e3dac6aefb8db2dbd1c651f0a2cf27b0f29559c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47734985"
---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>Microsoft Data Shaping Service para visão geral do OLE DB
> [!IMPORTANT]
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, os aplicativos devem usar XML.

 Microsoft Data Shaping Service para o provedor de serviço do OLE DB dá suporte à construção de hierárquica (formatado) [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos de um provedor de dados.

## <a name="provider-keyword"></a>Palavra-chave do provedor
 Para invocar o Data Shaping Service para OLE DB, especifique a seguinte palavra-chave e valor na cadeia de conexão.

```
"Provider=MSDataShape"
```

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 Quando esse provedor de serviço é chamado, as seguintes propriedades dinâmicas são adicionadas para o [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção da[Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.

|Nome da propriedade dinâmica|Description|
|---------------------------|-----------------|
|**Nomes de alterar de forma exclusiva**|Indica se **conjunto de registros** objetos com valores duplicados para seus **remodelar nome** propriedades são permitidas. Se essa propriedade dinâmica é **True** e um novo **conjunto de registros** é criado com o mesmo nome especificado pelo usuário a reformatação de uma existente **conjunto de registros**, em seguida, o novo  **Conjunto de registros** remodelagem nome de objeto é modificado para torná-lo exclusivo. Se essa propriedade for **falsos** e uma nova **conjunto de registros** é criado com o mesmo nome especificado pelo usuário a reformatação existente **conjunto de registros**, ambas as **conjunto de registros**  objetos terão o mesmo nome de reformatação. Portanto, nenhum dos dois **Recordset** pode ser reformatado desde que ambos os conjuntos de registros existem.<br /><br /> O valor padrão da propriedade é **falsos**.|
|**Provedor de dados**|Indica o nome do provedor que será fornecem linhas a ser formatada. Esse valor pode ser nenhum se um provedor não será usado para fornecer linhas.|

 Você também pode definir propriedades dinâmicas graváveis especificando seus nomes como palavras-chave na cadeia de conexão. Por exemplo, no Microsoft Visual Basic, defina a **provedor de dados** propriedade dinâmica a ser "MSDASQL", especificando:

```
Dim cn as New ADODB.Connection
cn.Open "Provider=MSDataShape;Data Provider=MSDASQL"
```

 Você também pode definir ou recuperar uma propriedade dinâmica especificando seu nome como o índice para o [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) propriedade. Por exemplo, o exemplo de código a seguir obtém e imprime o valor atual dos **provedor de dados** propriedades dinâmicas, em seguida, define um novo valor se cn. DataProvider foi definido como "MSDataShape" (direta ou indiretamente por meio da cadeia de caracteres de conexão) e a conexão não foi aberto:

```
Debug.Print cn.Properties("Data Provider")
cn.Properties("Data Provider") = "MSDASQL"
```

> [!NOTE]
>  A propriedade dinâmica, **provedor de dados**, podem ser definidas apenas em uma não abertos **Conexão** objeto. Depois que a conexão for aberta, o **provedor de dados** propriedade torna-se somente leitura.

 Para obter mais informações sobre formatação de dados, consulte [Data Shaping](../../../ado/guide/data/data-shaping-overview.md).

## <a name="see-also"></a>Consulte também
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
