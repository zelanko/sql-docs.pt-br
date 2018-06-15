---
title: Propriedade ParentURL (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::ParentURL
helpviewer_keywords:
- ParentURL property [ADO]
ms.assetid: 65120ce6-3900-4cd4-b322-3b9816d74737
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c4a0217d4f2e79dc5876af9518a06d73d2ac924d
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280650"
---
# <a name="parenturl-property-ado"></a>Propriedade ParentURL (ADO)
Indica uma cadeia de caracteres de URL absoluta que aponte para o pai [registro](../../../ado/reference/ado-api/record-object-ado.md) do atual **registro** objeto.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um **cadeia de caracteres** valor que indica a URL do pai **registro**.  
  
## <a name="remarks"></a>Remarks  
 O **ParentURL** propriedade depende da fonte usada para abrir o **registro** objeto. Por exemplo, o **registro** pode ser aberto com uma fonte que contém um nome de caminho relativo do diretório referenciado pelo [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade.  
  
 Suponha que o "depois" uma pasta está contida em "first". Abra o **registro** objeto usando a seguinte sintaxe:  
  
```  
record.ActiveConnection = "http://first"  
record.Open "second"  
```  
  
 Agora, o valor de `the` **ParentURL** é de propriedade `"http://first"`, o mesmo que **ActiveConnection**.  
  
 A fonte pode também ser uma URL absoluta, como `"http://first/second"`. O **ParentURL** é de propriedade, em seguida, `"http://first"`, o nível acima `"second"`.  
  
 Essa propriedade pode ser um valor nulo se:  
  
-   Não há nenhum pai para o objeto atual. Por exemplo, se o **registro** objeto representa a raiz de um diretório.  
  
-   O **registro** objeto representa uma entidade que não pode ser especificada com uma URL.  
  
 Esta propriedade é somente leitura.  
  
> [!NOTE]
>  Essa propriedade só é suportada pelos provedores de origem do documento, como o [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [registros e campos de Provider-Supplied](../../../ado/guide/data/records-and-provider-supplied-fields.md).  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [Absolute e URLs relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
> [!NOTE]
>  Se o registro atual contém um registro de dados do ADO **registros**, acessando o **ParentURL** propriedade faz com que um erro de tempo de execução, que indica que nenhuma URL, é possível.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
