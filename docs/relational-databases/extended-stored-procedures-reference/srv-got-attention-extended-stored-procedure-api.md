---
title: srv_got_attention (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_got_attention
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_got_attention
ms.assetid: 805e68e1-d17f-41bd-8b9f-a27283bb6fbe
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 02471fe1d955486e0ba17926dbf8bf042290b6b7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62671989"
---
# <a name="srvgotattention-extended-stored-procedure-api"></a>srv_got_attention (API do procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Verifica se a tarefa ou a conexão atual precisa ser anulada e retorna TRUE se a conexão for interrompida ou se o lote for anulado  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL srv_got_attention  
(SRV_PROC *  
srvproc  
);  
  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *srvproc*  
 Ponteiro que identifica uma conexão de banco de dados.  
  
## <a name="return-value"></a>Valor retornado  
 TRUE se a conexão for interrompida ou se o lote for anulado. FALSE se a conexão ou o lote estiverem ativos.  
  
## <a name="remarks"></a>Remarks  
 Um procedimento armazenado estendido de execução longa deve verificar a atenção do servidor chamando **srv_got_attention** periodicamente, de forma que o procedimento possa ser encerrado quando a conexão for interrompida ou o lote for anulado.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
