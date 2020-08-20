---
description: Tratamento de erro em Visual C++
title: Manipulando erros no Visual C++ | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- errors [ADO], Visual C++
- Visual C++ error handling [ADO]
ms.assetid: b7576f07-020a-45f7-9e79-b5756f33f7ab
author: rothja
ms.author: jroth
ms.openlocfilehash: 4b43b8314e47c8a96dadcf8cab841a37da0c0518
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453288"
---
# <a name="handling-errors-in-visual-c"></a>Tratamento de erro em Visual C++
No COM, a maioria das operações retorna um código de retorno HRESULT que indica se uma função foi concluída com êxito. A diretiva #import gera código wrapper em cada método "RAW" ou propriedade e verifica o HRESULT retornado. Se o HRESULT indicar falha, o código do wrapper lançará um erro COM chamando _com_issue_errorex () com o código de retorno HRESULT como um argumento. Objetos de erro COM podem ser capturados em um bloco **try-catch** . (Para fins de eficiência, pegue uma referência a um objeto _com_error.)  
  
 Lembre-se de que são erros do ADO: eles resultam da falha da operação do ADO. Os erros retornados pelo provedor subjacente aparecem como objetos de **erro** na coleção de **erros** do objeto de **conexão** .  
  
 A diretiva #import cria apenas rotinas de tratamento de erros para métodos e propriedades declarados no ADO. dll. No entanto, você pode aproveitar esse mesmo mecanismo de tratamento de erros escrevendo sua própria macro de verificação de erros ou função embutida. Consulte o tópico Visual C++® Extensions para obter exemplos.
