---
title: srv_rpcnumber (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_rpcnumber
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcnumber
ms.assetid: 3094085e-fe9e-423d-bf87-7852352c2d26
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1036cbe649a2448b3eb4838621ec8be0590b1c3a
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53372538"
---
# <a name="srvrpcnumber-extended-stored-procedure-api"></a>srv_rpcnumber (API de procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Retorna o componente de número da chamada do procedimento armazenado remoto atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_rpcnumber ( SRV_PROC *  
srvproc   
)  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que é o identificador de uma conexão de cliente específica (neste caso, o identificador que recebeu o procedimento armazenado remoto). A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
## <a name="returns"></a>Retorna  
 O componente de número do procedimento armazenado remoto atual. Se o cliente não usar um componente de número ao executar o procedimento armazenado remoto ou se não houver procedimento armazenado remoto atual, ele retornará - 1.  
  
## <a name="remarks"></a>Comentários  
 Esta função retorna apenas o componente de número do procedimento armazenado remoto. Ela não inclui os especificadores opcionais para proprietário, nome do procedimento armazenado remoto e nome do banco de dados.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
