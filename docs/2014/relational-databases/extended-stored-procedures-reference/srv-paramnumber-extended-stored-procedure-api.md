---
title: srv_paramnumber (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramnumber
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramnumber
ms.assetid: d7a6dbff-71d9-4297-8a4f-bfd2876fe204
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e957b4c775554869b04805f009d4daed4f1055a4
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53361558"
---
# <a name="srvparamnumber-extended-stored-procedure-api"></a>srv_paramnumber (API de procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Retorna o número de um parâmetro de chamada de procedimento armazenado remoto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_paramnumber (  
SRV_PROC *  
srvproc  
,  
DBCHAR *  
name  
,   
int  
namelen   
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que identifica uma conexão de cliente específica (nesse caso, o identificador que recebeu a chamada do procedimento armazenado remoto). A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *name*  
 É um ponteiro para o *name* do parâmetro.  
  
 *namelen*  
 É o tamanho total de *name*. Se *name* terminar em nulo, defina *namelen* como SRV_NULLTERM.  
  
## <a name="returns"></a>Retorna  
 O número do parâmetro nomeado. O primeiro parâmetro é 1. Se não houver nenhum parâmetro nomeado como *name* ou nenhum procedimento armazenado remoto, 0 será retornado e uma mensagem será gerada.  
  
## <a name="remarks"></a>Comentários  
 Quando uma chamada de procedimento armazenado remoto é feita com parâmetros, os parâmetros podem ser passados pelo nome ou pela posição (sem-nome). Se a chamada de procedimento armazenado remoto for feita com alguns parâmetros transmitidos pelo nome e outros pela posição, ocorrerá um erro. O manipulador SRV_RPC ainda é chamado, mas aparece como se não houvesse parâmetros e **srv_rpcparams** retorna 0.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte também  
 [srv_rpcparams &#40;API de Procedimento Armazenado Estendido&#41;](srv-rpcparams-extended-stored-procedure-api.md)  
  
  
