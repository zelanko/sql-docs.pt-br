---
title: srv_rpcoptions (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- srv_rpcoptions
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcoptions
ms.assetid: dbcce5d1-d5a1-4379-9597-04e43af5923d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 266c08c4e19d3cf2f3b2daebe3b6ac43ae0ca75e
ms.sourcegitcommit: 110e5e09ab3f301c530c3f6363013239febf0ce5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48905056"
---
# <a name="srvrpcoptions-extended-stored-procedure-api"></a>srv_rpcoptions (API de procedimento armazenado estendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Retorna opções de tempo de execução para o procedimento armazenado remoto atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DBUSMALLINT srv_rpcoptions ( SRV_PROC *  
srvproc   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que é o identificador de uma conexão de cliente específica (neste caso, o identificador que recebeu o procedimento armazenado remoto). A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
## <a name="returns"></a>Retorna  
 Um bitmap que contém os sinalizadores de tempo de execução unidos em um OU lógico para o procedimento armazenado remoto atual. Se não houver um procedimento armazenado remoto atual, será retornado 0 e uma mensagem é gerada.  
  
## <a name="remarks"></a>Remarks  
 A seguinte tabela descreve cada sinalizador de tempo de execução.  
  
|Sinalizador de tempo de execução|Descrição|  
|--------------------|-----------------|  
|SRV_NOMETADATA|O cliente solicitou resultados sem informações de metadados. Esse sinalizador é usado somente quando o cliente está se comunicando com uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um aplicativo de API de procedimento armazenado estendido não pode omitir informações de metadados.|  
|SRV_RECOMPILE|O cliente solicitou a recompilação do procedimento armazenado remoto antes de executá-lo. Este sinalizador pode não se aplicar a um aplicativo de API de procedimento armazenado estendido.|  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  
