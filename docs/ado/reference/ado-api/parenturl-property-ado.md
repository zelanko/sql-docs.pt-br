---
description: Propriedade ParentURL (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8254dd1e47d6f6d3042e88365bd3c6ad0ea4301f
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773235"
---
# <a name="parenturl-property-ado"></a>Propriedade ParentURL (ADO)
Indica uma cadeia de caracteres de URL absoluta que aponta para o [registro](./record-object-ado.md) pai do objeto de **registro** atual.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um valor de **cadeia de caracteres** que indica a URL do **registro**pai.  
  
## <a name="remarks"></a>Comentários  
 A propriedade **ParentURL** depende da fonte usada para abrir o objeto **Record** . Por exemplo, o **registro** pode ser aberto com uma fonte que contém um nome de caminho relativo de um diretório referenciado pela propriedade [ActiveConnection](./activeconnection-property-ado.md) .  
  
 Suponha que "Second" seja uma pasta contida em "First". Abra o objeto de **registro** usando a seguinte sintaxe:  
  
```  
record.ActiveConnection = "https://first"  
record.Open "second"  
```  
  
 Agora, o valor da `the` propriedade **ParentURL** é `"https://first"` igual a **ActiveConnection**.  
  
 A origem também pode ser uma URL absoluta, como, `"https://first/second"` . Em seguida, a propriedade **ParentURL** é `"https://first"` o nível acima `"second"` .  
  
 Essa propriedade pode ser um valor nulo se:  
  
-   Não há nenhum pai para o objeto atual; por exemplo, se o objeto **Record** representa a raiz de um diretório.  
  
-   O objeto **Record** representa uma entidade que não pode ser especificada com uma URL.  
  
 Esta propriedade é somente para leitura.  
  
> [!NOTE]
>  Essa propriedade só tem suporte por provedores de origem de documento, como o [provedor de OLE DB da Microsoft para publicação na Internet](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [registros e campos fornecidos pelo provedor](../../guide/data/records-and-provider-supplied-fields.md).  
  
> [!NOTE]
>  As URLs que usam o esquema http invocarão automaticamente o [provedor do Microsoft OLE DB para publicação na Internet](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [URLs absolutas e relativas](../../guide/data/absolute-and-relative-urls.md).  
  
> [!NOTE]
>  Se o registro atual contiver um registro de dados de um **conjunto de registros**ADO, o acesso à propriedade **ParentURL** causará um erro em tempo de execução, indicando que nenhuma URL é possível.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Record (ADO)](./record-object-ado.md)