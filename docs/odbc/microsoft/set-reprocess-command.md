---
title: DEFINIR o REPROCESSAMENTO comando | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SET REPROCESS command [ODBC]
ms.assetid: b0708757-b1d7-42f3-8988-787f2a806b8b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 560d6b98c27cefe438e99e2948decaded827e618
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="set-reprocess-command"></a>Comando de REPROCESSAMENTO do conjunto
Especifica quantas vezes ou como longos para bloquear um arquivo ou um registro após uma tentativa malsucedida de bloqueio.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>Argumentos  
 PARA *nAttempts*[SECONDS]  
 Especifica o número de vezes ou o número de segundos para tentar bloquear um arquivo ou registro após a tentativa inicial sem êxito. O valor padrão é 0; o valor máximo é 32.000.  
  
 SEGUNDOS Especifica que o Visual FoxPro tenta bloquear um arquivo de registro ou de *nAttempts* segundos. Ele está disponível apenas quando *nAttempts* é maior que zero.  
  
 Por exemplo, se *nAttempts* é 30, Visual FoxPro tenta bloquear um registro ou de arquivos até 30 vezes. Se você também pode incluir segundos (definir REPROCESSAR a 30 segundos), do Visual FoxPro continuamente tenta bloquear um arquivo ou registro de até 30 segundos.  
  
 Se um erro de ON a rotina está em vigor e tentativas por um comando para bloquear o registro ou o arquivo não forem bem-sucedidas, a rotina de erro ON é executada. No entanto, se o bloqueio de tentativas de uma função, uma rotina de erro ON não é executada e a função retornará False (. F.).  
  
 Se uma rotina de erro ON não está em vigor, um comando tenta bloquear o registro ou o arquivo e o bloqueio não pode ser colocado, um erro será gerado. Se uma função tenta colocar o bloqueio, o alerta não será exibido e a função retornará False (. F.).  
  
 Se *nAttempts* é 0 (o valor padrão) e emitir um comando ou função que tenta bloquear um arquivo ou registro, Visual FoxPro tenta bloquear o registro ou arquivo indefinidamente. Se o registro ou o arquivo se torna disponível para enquanto espera de bloqueio, o bloqueio é colocado e a mensagem do sistema está desmarcada. Se uma função de tentativa de colocar o bloqueio, a função retornará verdadeiro (. T.).  
  
 Se um erro de ON a rotina está em vigor e um comando está tentando bloquear o registro ou o arquivo, a rotina de erro ON prevalece sobre tentativas adicionais para bloquear o registro ou o arquivo. A rotina de erro ON é executada imediatamente. Do Visual FoxPro não tentará um registro adicional ou bloqueios de arquivo e não exibe a mensagem do sistema.  
  
 Se *nAttempts* é 1, Visual FoxPro tenta bloquear o registro ou arquivo indefinidamente e uma rotina de erro ON não é executada.  
  
 Se um bloqueio foi colocado por outro usuário no arquivo que você está tentando bloquear ou registro, você deve aguardar até que o usuário libera o bloqueio.  
  
 COMO AUTOMÁTICO  
 Especifica que o Visual FoxPro tenta bloquear o registro ou arquivo indefinidamente. (O REPROCESSAMENTO de conjunto para -2 é um comando equivalente).  
  
## <a name="remarks"></a>Comentários  
 A primeira tentativa de bloquear um arquivo ou registro nem sempre é bem-sucedida. Frequentemente, um registro ou o arquivo está bloqueado por outro usuário na rede. Definir REPROCESSAR determina se do Visual FoxPro faz tentativas adicionais para bloquear o registro ou o arquivo quando a tentativa inicial for bem-sucedida. Você pode especificar quantas vezes tentativas adicionais são feitas ou quanto tempo as tentativas são feitas. Uma rotina de erro ON afeta como malsucedido bloqueio tentativas são tratadas.

