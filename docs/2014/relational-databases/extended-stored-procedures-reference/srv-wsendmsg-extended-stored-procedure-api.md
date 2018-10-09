---
title: srv_wsendmsg (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- srv_wsendmsg
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_wsendmsg
ms.assetid: f2153076-32c9-4a52-8e1b-fc9618153543
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 391388b7842395319bac80fd76cf2cd5c37f56ad
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48100166"
---
# <a name="srvwsendmsg-extended-stored-procedure-api"></a>srv_wsendmsg (API do procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Envia uma mensagem de Unicode ao cliente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_wsendmsg(SRV_PROC *   
srvproc  
, int   
msgnum  
, int   
severity  
, WCHAR *   
message  
, int   
msglen  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que atua como identificador de uma conexão de cliente específica. A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *Msgnum*  
 É um número de mensagem de 4 bytes.  
  
 *Severity*  
 Especifica a gravidade do erro. Uma gravidade menor ou igual a 10 é considerada uma mensagem informativa. Caso contrário, trata-se de um erro.  
  
 *message*  
 É um ponteiro para a cadeia de caracteres de Unicode que será enviada ao cliente.  
  
 *msglen*  
 Especifica o comprimento, em caracteres, de *message*.  
  
## <a name="returns"></a>Retorna  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
 Use esta função para enviar mensagens em Unicode. É semelhante a **srv_sendmsg**, mas a mensagem que envia é uma cadeia de caracteres de WCHAR em vez de uma cadeia de caracteres de DBCHAR. Observe que o comprimento da mensagem é informado em caracteres, e não em bytes, e que *msglen* nunca será igual a SRV_NULLTERM.  
  
 A função retorna FAIL quando  
  
-   O *msglen* fornecido não está no intervalo de 0-32242.  
  
-   O *msglen* fornecido é 0, mas o ponteiro de mensagem é o NULL.  
  
-   Ocorre um erro ao enviar a mensagem de erro na rede.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte também  
 [srv_sendmsg &#40;API de Procedimento Armazenado Estendido&#41;](srv-sendmsg-extended-stored-procedure-api.md)  
  
  
