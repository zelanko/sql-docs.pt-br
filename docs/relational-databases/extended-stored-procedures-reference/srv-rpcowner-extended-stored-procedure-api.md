---
title: srv_rpcowner (API de Procedimento Armazenado Estendido) | Microsoft Docs
description: Saiba como srv_rpcowner na API de procedimento armazenado estendido retorna o componente de proprietário para o procedimento armazenado remoto atual.
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_rpcowner
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcowner
ms.assetid: e81a60e6-14ea-47bc-a11c-3d7635344447
author: rothja
ms.author: jroth
ms.openlocfilehash: 64e9fa0970367ccac5d4fca5bf6b9815ad0e0e17
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248265"
---
# <a name="srv_rpcowner-extended-stored-procedure-api"></a>srv_rpcowner (API de procedimento armazenado estendido)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Retorna o componente proprietário de procedimento para o procedimento armazenado remoto atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DBCHAR * srv_rpcowner (  
SRV_PROC *  
srvproc  
,  
int *  
len   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que é o identificador de uma conexão de cliente específica (neste caso, o identificador que recebeu o procedimento armazenado remoto). A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *Len*  
 É um ponteiro para uma variável inteira que recebe o comprimento do nome do proprietário. O parâmetro *len* pode ser NULL, caso em que o tamanho do componente do proprietário não é retornado.  
  
## <a name="returns"></a>Retornos  
 Um ponteiro DBCHAR ponteiro para o componente do proprietário com terminação nula para o procedimento armazenado remoto atual. Se não houver um procedimento armazenado remoto atual, NULL será retornado e *len* será definido como -1.  
  
## <a name="remarks"></a>Comentários  
 Essa função retorna apenas o componente proprietário do procedimento armazenado remoto. Ela não inclui os especificadores opcionais para nome, nome de procedimento armazenado remoto e número de procedimento armazenado remoto.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
