---
description: Capturar códigos de erro do ADO
title: Códigos de erro do ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], error codes
ms.assetid: 3aee61c7-a9b7-4596-b78e-5828a00d0281
author: rothja
ms.author: jroth
ms.openlocfilehash: 2502e1dec35ec0d6450190650a18ac765ce14421
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88355222"
---
# <a name="capture-ado-error-codes"></a>Capturar códigos de erro do ADO
Além dos erros de provedor retornados nos objetos de [erro](../../../ado/reference/ado-api/error-object.md) da coleção de [erros](../../../ado/reference/ado-api/errors-collection-ado.md) , o próprio ADO pode retornar erros ao mecanismo de tratamento de exceções do seu ambiente de tempo de execução. Use o mecanismo de interceptação de erros de sua linguagem de programação, como a instrução **On Error** no Microsoft® Visual Basic ou o bloco **try-catch** em Microsoft Visual C++®, para capturar erros do ADO.

 Para obter a lista de códigos de erro do ADO, consulte [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md).

## <a name="see-also"></a>Consulte Também
 [Error Object](../../../ado/reference/ado-api/error-object.md) [Coleção de erros de objeto de erro (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)
