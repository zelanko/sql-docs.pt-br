---
title: Provedor de persistência do Microsoft OLE DB (provedor de serviços ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB persistence provider
- persistence provider [ADO]
- OLE DB persistence provider [ADO]
ms.assetid: e75ef0dc-2016-4fcc-8918-23311c0d4e02
author: rothja
ms.author: jroth
ms.openlocfilehash: cc8c8f099e703433f57e9d8ff463e229213503be
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758462"
---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Visão geral do provedor de persistência da Microsoft OLE DB
O provedor de persistência da Microsoft OLE DB permite que você salve um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) em um arquivo e, posteriormente, restaure esse objeto **Recordset** a partir do arquivo. Informações de esquema, dados e alterações pendentes são preservadas.

 Você pode salvar o **conjunto de registros** no formato de ADTG (grama de tabela de dados avançada) proprietário ou no formato de linguagem XML aberto (XML).

## <a name="provider-keyword"></a>Palavra-chave Provider
 Para invocar esse provedor, especifique a palavra-chave e o valor a seguir na cadeia de conexão.

```vb
"Provider=MSPersist"
```

## <a name="errors"></a>Errors
 Os seguintes erros emitidos por esse provedor podem ser detectados em seu aplicativo.

|Constante|Description|
|--------------|-----------------|
|E_BADSTREAM|O arquivo aberto não tem um formato válido (ou seja, o formato não é ADTG ou XML).|
|E_CANTPERSISTROWSET|O objeto **Recordset** salvo tem características que impedem que ele seja armazenado.|

## <a name="remarks"></a>Comentários
 O provedor de persistência do Microsoft OLE DB não expõe propriedades dinâmicas.

 No momento, somente objetos **Recordset** hierárquicos com parâmetros não podem ser salvos.

 Para obter mais informações sobre o armazenamento persistente de objetos do **conjunto de registros** , consulte persistência do [conjunto de registros](../../../ado/guide/data/more-about-recordset-persistence.md).

 Quando um fluxo é usado para abrir um **conjunto de registros,** não deve haver nenhum parâmetro especificado além do parâmetro de *origem* do método **Open** .

## <a name="see-also"></a>Consulte Também
[Provedor de persistência do Microsoft OLE DB (provedor de serviços ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)
