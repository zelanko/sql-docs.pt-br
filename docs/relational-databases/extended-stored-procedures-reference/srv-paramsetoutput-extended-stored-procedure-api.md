---
title: srv_paramsetoutput (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- srv_paramsetoutput
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramsetoutput
ms.assetid: f2810e19-e513-458b-8925-5756b6ee1313
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f2436a716d379cb9a5d9eef61d628b8ffed59720
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="srvparamsetoutput-extended-stored-procedure-api"></a>srv_paramsetoutput (API de procedimento armazenado estendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use a integração CLR em vez disso.  
  
 Define o valor de um parâmetro de retorno. Essa função substitui a função **srv_paramset**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_paramsetoutput (  
SRV_PROC *  
srvproc  
,  
int  
n  
,  
BYTE *  
pbData  
,  
ULONG   
cbLen  
,  
BOOL  
fNull   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um identificador para uma conexão do cliente.  
  
 *n*  
 É o número ordinal do parâmetro que será definido. O primeiro parâmetro é 1.  
  
 *pbData*  
 É um ponteiro para o valor dos dados que será enviado de volta ao cliente como um parâmetro de retorno do procedimento.  
  
 *cbLen*  
 É o comprimento real dos dados que serão retornados. Se o tipo de dados do parâmetro especificar valores de um tamanho constante e não permitir valores nulos (por exemplo, *srvbit* ou *srvint1*), *cbLen* será ignorado. Um valor igual a 0 significará dados de comprimento zero se *fNull* for FALSE.  
  
 *fNull*  
 É um sinalizador que indica se o valor do parâmetro de retorno é o NULL. Defina este sinalizador como TRUE se o parâmetro for definido como NULL. O valor padrão é FALSE. Se *fNull* for definido como TRUE, *cbLen* deverá ser definido como 0 ou a função falhará.  
  
## <a name="returns"></a>Retorna  
 Se as informações de parâmetro tiverem sido definidas com êxito, SUCCEED será retornado. Caso contrário, o retorno será FAIL. FAIL é retornado quando  
  
-   o parâmetro não é um parâmetro de retorno ou  
  
-   o argumento *cbLen* é inválido.  
  
## <a name="remarks"></a>Remarks  
 **Observação de segurança** Você deve examinar detalhadamente o código-fonte de procedimentos armazenados estendidos e testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  
