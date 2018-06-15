---
title: Provedor de persistência do Microsoft OLE DB (provedor de serviços de ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB persistence provider
- persistence provider [ADO]
- OLE DB persistence provider [ADO]
ms.assetid: e75ef0dc-2016-4fcc-8918-23311c0d4e02
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37144f19abfb60d13a24818d8b47a3531affcc08
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270385"
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

## <a name="remarks"></a>Remarks
 O Microsoft OLE DB provedor de persistência não expõe nenhum propriedades dinâmicas.

 Atualmente, apenas parametrizados hierárquica **registros** objetos não podem ser salvos.

 Para obter mais informações sobre o armazenamento de maneira persistente **registros** objetos, consulte [persistência de conjunto de registros](../../../ado/guide/data/more-about-recordset-persistence.md).

 Quando um fluxo é usado para abrir um **conjunto de registros,** não deve haver nenhum parâmetro especificado que o *fonte* parâmetro do **abrir** método.

## <a name="see-also"></a>Consulte também
[Provedor de persistência do Microsoft OLE DB (provedor de serviços de ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)
