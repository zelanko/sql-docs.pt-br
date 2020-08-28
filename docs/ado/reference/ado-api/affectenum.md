---
description: AffectEnum
title: AffectEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AffectEnum
helpviewer_keywords:
- AffectEnum enumeration [ADO]
ms.assetid: 1ab921a0-6c57-43b4-9291-701b2599f3e8
author: rothja
ms.author: jroth
ms.openlocfilehash: 9673567c17cda79c93fba4e74b104bd0cb42edd7
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976137"
---
# <a name="affectenum"></a>AffectEnum
Especifica quais registros são afetados por uma operação.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adAffectAll**|3|Se não houver um [filtro](./filter-property.md) aplicado ao conjunto de **registros**, o afetará todos os registros.<br /><br /> Se a propriedade **Filter** for definida como um critério de cadeia de caracteres (como "Author = ' Smith '"), a operação afetará os registros visíveis no capítulo atual.<br /><br /> Se a propriedade **Filter** for definida como um membro de [FilterGroupEnum](./filtergroupenum.md) ou uma matriz de indicadores, a operação afetará todas as linhas do **conjunto de registros**. **Observação: adAffectAll** está oculto no Pesquisador de objetos Visual Basic.|  
|**adAffectAllChapters**|4|Afeta todos os registros em todos os capítulos irmãos do **conjunto de registros**, incluindo aqueles não visíveis por meio de qualquer **filtro** aplicado no momento.|  
|**adAffectCurrent**|1|Afeta apenas o registro atual.|  
|**adAffectGroup**|2|Afeta somente os registros que atendem à configuração de propriedade de [filtro](./filter-property.md) atual. Você deve definir a propriedade de **filtro** para um valor **FilterGroupEnum** ou uma matriz de **indicadores** para usar essa opção.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. afeta. ALL|  
|AdoEnums. afeto. os capítulos|  
|AdoEnums. afeto. CURRENT|  
|AdoEnums. afetou. GROUP|  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Método CancelBatch (ADO)](./cancelbatch-method-ado.md)  
        [Método Delete (Conjunto de registros ADO)](./delete-method-ado-recordset.md)  
    :::column-end:::
    :::column:::
        [Método Resync](./resync-method.md)  
        [Método UpdateBatch](./updatebatch-method.md)  
    :::column-end:::
:::row-end:::