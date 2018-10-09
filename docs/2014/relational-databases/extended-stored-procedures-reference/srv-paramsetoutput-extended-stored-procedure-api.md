---
title: srv_paramsetoutput (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- srv_paramsetoutput
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramsetoutput
ms.assetid: f2810e19-e513-458b-8925-5756b6ee1313
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bf5e962de42509eab06e2077de19e668efbc754f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48212466"
---
# <a name="srvparamsetoutput-extended-stored-procedure-api"></a>srv_paramsetoutput (API de procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
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
  
## <a name="remarks"></a>Comentários  
 **Observação de segurança** Você deve examinar detalhadamente o código-fonte de procedimentos armazenados estendidos e testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  
