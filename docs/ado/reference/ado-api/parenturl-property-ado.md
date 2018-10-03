---
title: Propriedade ParentURL (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::ParentURL
helpviewer_keywords:
- ParentURL property [ADO]
ms.assetid: 65120ce6-3900-4cd4-b322-3b9816d74737
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fdbff500a90ab4456b3e9ef252be4407c636cdec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47822104"
---
# <a name="parenturl-property-ado"></a>Propriedade ParentURL (ADO)
Indica uma cadeia de caracteres de URL absoluta que aponta para o pai [registro](../../../ado/reference/ado-api/record-object-ado.md) atual **registro** objeto.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um **cadeia de caracteres** valor que indica a URL do pai **registro**.  
  
## <a name="remarks"></a>Comentários  
 O **ParentURL** propriedade depende da fonte usada para abrir o **registro** objeto. Por exemplo, o **registro** pode ser aberto com uma fonte que contém um nome de caminho relativo de um diretório referenciado pelo [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade.  
  
 Suponha que o "segundo" é uma pasta é contida em "primeiro". Abra o **registro** objeto usando a sintaxe a seguir:  
  
```  
record.ActiveConnection = "http://first"  
record.Open "second"  
```  
  
 Agora, o valor de `the` **ParentURL** é de propriedade `"http://first"`, o mesmo que **ActiveConnection**.  
  
 O código-fonte também pode ser uma URL absoluta, como `"http://first/second"`. O **ParentURL** propriedade é então `"http://first"`, o nível acima `"second"`.  
  
 Essa propriedade pode ser um valor nulo se:  
  
-   Não há nenhum pai para o objeto atual. Por exemplo, se o **registro** objeto representa a raiz de um diretório.  
  
-   O **registro** objeto representa uma entidade que não pode ser especificada com uma URL.  
  
 Esta propriedade é somente leitura.  
  
> [!NOTE]
>  Essa propriedade só é suportada por provedores de código-fonte do documento, como o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [registros e campos de Provider-Supplied](../../../ado/guide/data/records-and-provider-supplied-fields.md).  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [absoluta e relativa URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
> [!NOTE]
>  Se o registro atual contém um registro de dados do ADO **conjunto de registros**, o acesso a **ParentURL** propriedade faz com que um erro de tempo de execução, que indica que nenhuma URL, é possível.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
