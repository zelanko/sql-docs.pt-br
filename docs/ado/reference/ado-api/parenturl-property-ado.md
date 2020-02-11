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
ms.openlocfilehash: 54b2db44fe2e1971356f96d33aa8de0b02781b1e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931648"
---
# <a name="parenturl-property-ado"></a>Propriedade ParentURL (ADO)
Indica uma cadeia de caracteres de URL absoluta que aponta para o [registro](../../../ado/reference/ado-api/record-object-ado.md) pai do objeto de **registro** atual.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um valor de **cadeia de caracteres** que indica a URL do **registro**pai.  
  
## <a name="remarks"></a>Comentários  
 A propriedade **ParentURL** depende da fonte usada para abrir o objeto **Record** . Por exemplo, o **registro** pode ser aberto com uma fonte que contém um nome de caminho relativo de um diretório referenciado pela propriedade [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) .  
  
 Suponha que "Second" seja uma pasta contida em "First". Abra o objeto de **registro** usando a seguinte sintaxe:  
  
```  
record.ActiveConnection = "https://first"  
record.Open "second"  
```  
  
 Agora, o valor da `the` propriedade **ParentURL** é `"https://first"`igual a **ActiveConnection**.  
  
 A origem também pode ser uma URL absoluta, como, `"https://first/second"`. Em **** seguida `"https://first"`, a propriedade ParentURL é o nível `"second"`acima.  
  
 Essa propriedade pode ser um valor nulo se:  
  
-   Não há nenhum pai para o objeto atual; por exemplo, se o objeto **Record** representa a raiz de um diretório.  
  
-   O objeto **Record** representa uma entidade que não pode ser especificada com uma URL.  
  
 Essa propriedade é somente leitura.  
  
> [!NOTE]
>  Essa propriedade só tem suporte por provedores de origem de documento, como o [provedor de OLE DB da Microsoft para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [registros e campos fornecidos pelo provedor](../../../ado/guide/data/records-and-provider-supplied-fields.md).  
  
> [!NOTE]
>  As URLs que usam o esquema http invocarão automaticamente o [provedor do Microsoft OLE DB para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [URLs absolutas e relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
> [!NOTE]
>  Se o registro atual contiver um registro de dados de um **conjunto de registros**ADO, o acesso à propriedade **ParentURL** causará um erro em tempo de execução, indicando que nenhuma URL é possível.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
