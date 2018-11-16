---
title: Persistência do Microsoft OLE DB Provider (provedor de serviços do ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2550e36f977be13e10865d4bd238c8508c542091
ms.sourcegitcommit: 96b2355d54dfad259826e88bdff91cc9344e16f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51350001"
---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Visão geral do provedor de persistência OLE DB da Microsoft
O Microsoft OLE DB provedor de persistência permite que você salve uma [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) em um arquivo de objeto e restaurá-lo mais tarde **Recordset** objeto do arquivo. Informações de esquema, dados e as alterações pendentes são preservados.

 Você pode salvar a **Recordset** no formato de grama de tabela de dados avançado (ADTG) o proprietário ou formato aberto Extensible Markup Language (XML).

## <a name="provider-keyword"></a>Palavra-chave do provedor
 Para invocar esse provedor, especifique a seguinte palavra-chave e valor na cadeia de conexão.

```vb
"Provider=MSPersist"
```

## <a name="errors"></a>Erros
 Os seguintes erros emitidos por esse provedor podem ser detectados em seu aplicativo.

|Constante|Description|
|--------------|-----------------|
|E_BADSTREAM|O arquivo aberto não tem um formato válido (ou seja, o formato não é ADTG ou XML).|
|E_CANTPERSISTROWSET|O **Recordset** objeto salvo tem características que impedem a serem armazenados.|

## <a name="remarks"></a>Comentários
 O Microsoft OLE DB provedor de persistência não expõe nenhuma propriedade dinâmica.

 Atualmente, apenas com parâmetros hierárquicos **Recordset** objetos não podem ser salvos.

 Para obter mais informações sobre como armazenar persistentemente **conjunto de registros** objetos, consulte [persistência de conjunto de registros](../../../ado/guide/data/more-about-recordset-persistence.md).

 Quando um fluxo é usado para abrir um **conjunto de registros,** não deve haver nenhum parâmetro especificado diferente das *fonte* parâmetro do **abrir** método.

## <a name="see-also"></a>Consulte também
[Persistência do Microsoft OLE DB Provider (provedor de serviços do ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)
