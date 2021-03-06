---
description: Propriedade Prepared (ADO)
title: Propriedade preparada (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Prepared
helpviewer_keywords:
- Prepared property [ADO]
ms.assetid: 11ca8825-765e-4bb4-a6ce-3f6564ad8755
author: rothja
ms.author: jroth
ms.openlocfilehash: 7352d21467061a38bd7e2443ecb52fdb59bd7696
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990037"
---
# <a name="prepared-property-ado"></a>Propriedade Prepared (ADO)
Indica se deve salvar uma versão compilada de um [comando](./command-object-ado.md) antes da execução.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **booliano** que, se definido como **true**, indica que o comando deve ser preparado.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **preparada** para fazer com que o provedor salve uma versão preparada (ou compilada) da consulta especificada na propriedade [CommandText](./commandtext-property-ado.md) antes da primeira execução de um objeto de [comando](./command-object-ado.md) . Isso pode retardar a primeira execução de um comando, mas depois que o provedor compilar um comando, o provedor usará a versão compilada do comando para todas as execuções subsequentes, o que resultará em um desempenho aprimorado.  
  
 Se a propriedade for **false**, o provedor executará o objeto de **comando** diretamente sem criar uma versão compilada.  
  
 Se o provedor não oferecer suporte à preparação de comando, ele poderá retornar um erro quando essa propriedade for definida como **true**. Se o provedor não retornar um erro, ele simplesmente ignorará a solicitação para preparar o comando e definirá a propriedade **preparada** como **false**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Command (ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade preparada (VB)](./prepared-property-example-vb.md)   
 [Exemplo da propriedade Prepared (VC++)](./prepared-property-example-vc.md)