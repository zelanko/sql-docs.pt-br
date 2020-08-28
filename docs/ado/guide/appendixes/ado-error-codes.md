---
description: Capturar códigos de erro do ADO
title: Códigos de erro do ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], error codes
ms.assetid: 3aee61c7-a9b7-4596-b78e-5828a00d0281
author: rothja
ms.author: jroth
ms.openlocfilehash: aa933f7be33f564af3aaf2851f6ec32bd5b4c5d4
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991177"
---
# <a name="capture-ado-error-codes"></a>Capturar códigos de erro do ADO
Além dos erros de provedor retornados nos objetos de [erro](../../reference/ado-api/error-object.md) da coleção de [erros](../../reference/ado-api/errors-collection-ado.md) , o próprio ADO pode retornar erros ao mecanismo de tratamento de exceções do seu ambiente de tempo de execução. Use o mecanismo de interceptação de erros de sua linguagem de programação, como a instrução **On Error** no Microsoft® Visual Basic ou o bloco **try-catch** em Microsoft Visual C++®, para capturar erros do ADO.

 Para obter a lista de códigos de erro do ADO, consulte [ErrorValueEnum](../../reference/ado-api/errorvalueenum.md).

## <a name="see-also"></a>Consulte Também
 [Error Object](../../reference/ado-api/error-object.md) [Coleção de erros de objeto de erro (ADO)](../../reference/ado-api/errors-collection-ado.md)