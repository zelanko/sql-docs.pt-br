---
title: srv_sendrow (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_sendrow
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_sendrow
ms.assetid: a08f608a-10e6-4bff-9b48-0d02e8026cdb
author: rothja
ms.author: jroth
ms.openlocfilehash: 47bfaa2ceb0885379bd5633f0160d2a9b24cf3c4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036027"
---
# <a name="srv_sendrow-extended-stored-procedure-api"></a>srv_sendrow (API de procedimento armazenado estendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Em vez disso, use a integração CLR.  
  
 Transmite uma linha de dados ao cliente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_sendrow ( SRV_PROC *  
srvproc   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que é o identificador de uma conexão de cliente específica (neste caso, o identificador que recebeu a solicitação de linguagem). A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
## <a name="returns"></a>Retornos  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
 A função **srv_sendrow** é chamada uma vez para cada linha enviada ao cliente. Todas as linhas devem ser enviadas ao cliente antes de qualquer mensagem, valor de status ou status de conclusão ser enviado com **srv_sendmsg**, **srv_status**ou **srv_senddone**.  
  
 O envio de uma linha que não tenha tido todas as suas colunas definidas com **srv_describe** faz com que o aplicativo da API de Procedimento Armazenado Estendido crie uma mensagem de erro informativa e retorne FAIL ao cliente. Neste caso, a linha não é enviada.  
  
> [!NOTE]  
>  A API de Procedimento Armazenado Estendido não dá suporte ao envio de linhas computadas ao cliente. Além disso, se uma linha que contenha dados **ntext**, **text**ou **image** for enviada ao cliente, o ponteiro de texto e o carimbo de data/hora de texto não serão incluídos.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte Também  
 [srv_describe &#40;API de procedimento armazenado estendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
