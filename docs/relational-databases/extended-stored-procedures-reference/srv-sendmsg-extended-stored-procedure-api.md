---
title: srv_sendmsg (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_sendmsg
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_sendmsg
ms.assetid: efcb50b9-f8ff-4121-bf67-05830171b928
author: rothja
ms.author: jroth
ms.openlocfilehash: 62fa2db01ff17008a0b6a7cd4e5fd0a2bce71189
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67910908"
---
# <a name="srv_sendmsg-extended-stored-procedure-api"></a>srv_sendmsg (API do procedimento armazenado estendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Em vez disso, use a integração CLR.  
  
 Envia uma mensagem ao cliente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_sendmsg (  
SRV_PROC *  
srvproc  
,  
int  
msgtype  
,  
DBINT  
msgnum  
,  
DBTINYINT  
class  
,   
DBTINYINT  
state  
,  
DBCHAR *  
rpcname  
,  
int   
rpcnamelen  
,  
DBUSMALLINT  
linenum  
,  
DBCHAR *  
message  
,  
int  
msglen   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que é o identificador de uma conexão de cliente específica (neste caso, o identificador que recebeu a solicitação de linguagem). A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *msgtype*  
 É SRV_MSG_INFO ou SRV_MSG_ERROR, dependendo se o servidor está enviando uma mensagem informativa ou de erro.  
  
 *msgnum*  
 É um número de mensagem de 4 bytes.  
  
 *class*  
 Especifica a gravidade do erro. Uma gravidade menor ou igual a 10 é considerada uma mensagem informativa.  
  
 *status*  
 Fornece o número do estado de erro para a mensagem atual. O número do estado de erro fornece informações sobre o contexto do erro. Os números de estado válidos variam de 0 a 255.  
  
 *rpcname*  
 Atualmente ele não tem suporte.  
  
 *rpcnamelen*  
 Atualmente ele não tem suporte.  
  
 *linenum*  
 É o número da linha no lote de comando de linguagem onde a mensagem é aplicada. Os números da linha iniciam em 1. Se *linenum* não se aplicar à mensagem, defina-o como 0.  
  
 *Mensagem*  
 É um ponteiro para a cadeia de caracteres que será enviada ao cliente.  
  
 *msglen*  
 Especifica o tamanho, em bytes, de *message*. Se *message* terminar em nulo, defina *msglen* como SRV_NULLTERM.  
  
## <a name="returns"></a>Retornos  
 SUCCEED ou FAIL  
  
## <a name="remarks"></a>Comentários  
 Essa função envia mensagens de erro ou informativas ao cliente. Ela é chamada uma vez para cada mensagem que será enviada.  
  
 É possível enviar mensagens ao cliente com **srv_sendmsg** em qualquer ordem antes ou depois que todas as linhas (se houver) tiverem sido enviadas com **srv_sendrow**. Todas as mensagens, se houver, devem ser enviadas ao cliente antes do envio do status de conclusão com **srv_senddone**.  
  
 Para enviar mensagens em Unicode, use **srv_wsendmsg** no lugar de **srv_sendmsg**.  
  
 Para obter mais informações [, consulte dados Unicode e páginas de código do servidor](../../relational-databases/extended-stored-procedures-programming/unicode-data-and-server-code-pages.md).  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
