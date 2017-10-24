---
title: "Provedor de persistência do Microsoft OLE DB (provedor de serviços de ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], OLE DB persistence provider
- persistence provider [ADO]
- OLE DB persistence provider [ADO]
ms.assetid: e75ef0dc-2016-4fcc-8918-23311c0d4e02
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 508b983c514031587f2b6507b806d3f279e0f822
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Visão geral do provedor de persistência OLE DB da Microsoft
O Microsoft OLE DB provedor de persistência permite que você salve uma [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto em um arquivo e, em seguida, restaurá-lo mais tarde **registros** objeto do arquivo. Informações de esquema, dados e as alterações pendentes serão preservadas.

 Você pode salvar o **registros** no formato proprietário Gram de tabela de dados avançado (ADTG) ou o formato aberto do Extensible Markup Language (XML).

## <a name="provider-keyword"></a>Palavra-chave do provedor
 Para chamar esse provedor, especifique a seguinte palavra-chave e valor na cadeia de conexão.

```
"Provider=MSPersist"
```

## <a name="errors"></a>Erros
 Os erros a seguir emitidos por esse provedor podem ser detectados em seu aplicativo.

|Constante|Description|
|--------------|-----------------|
|E_BADSTREAM|O arquivo aberto não tem um formato válido (ou seja, o formato não é ADTG ou XML).|
|E_CANTPERSISTROWSET|O **registros** objeto salvo tem características que impedem que está sendo armazenado.|

## <a name="remarks"></a>Comentários
 O Microsoft OLE DB provedor de persistência não expõe nenhum propriedades dinâmicas.

 Atualmente, apenas parametrizados hierárquica **registros** objetos não podem ser salvos.

 Para obter mais informações sobre o armazenamento de maneira persistente **registros** objetos, consulte [persistência de conjunto de registros](../../../ado/guide/data/more-about-recordset-persistence.md).

 Quando um fluxo é usado para abrir um **conjunto de registros,** não deve haver nenhum parâmetro especificado que o *fonte* parâmetro do **abrir** método.

## <a name="see-also"></a>Consulte também
[Provedor de persistência do Microsoft OLE DB (provedor de serviços de ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)

