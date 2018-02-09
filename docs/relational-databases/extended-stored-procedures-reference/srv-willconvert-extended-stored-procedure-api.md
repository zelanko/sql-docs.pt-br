---
title: srv_willconvert (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
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
- srv_willconvert
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_willconvert
ms.assetid: 6f4db5fd-215a-461c-95e4-17697852733e
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e4a39602f8e7e75dabacbac405758aee6879b0b2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="srvwillconvert-extended-stored-procedure-api"></a>srv_willconvert (API de procedimento armazenado estendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use a integração CLR em vez disso.  
  
 Determina se uma conversão de tipo de dados específica está disponível na Biblioteca ODS.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL srv_willconvert (  
int  
srctype  
,  
int  
desttype   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srctype*  
 Indica o tipo dos dados a serem convertidos. Este parâmetro pode ser qualquer dos tipos de dados de API de procedimento armazenado estendido.  
  
 *desttype*  
 Indica o tipo de dados no qual os dados de origem são convertidos. Este parâmetro pode ser qualquer dos tipos de dados de API de procedimento armazenado estendido.  
  
## <a name="returns"></a>Retorna  
 TRUE se houver suporte para a conversão de tipo de dados; FALSE se não houver suporte para a conversão de tipos de dados.  
  
## <a name="remarks"></a>Remarks  
 Para obter uma descrição de cada tipo de dados, consulte [Tipos de dados &#40;API de Procedimento Armazenado Estendido&#41;](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md).  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte também  
 [srv_convert &#40;API de Procedimento Armazenado Estendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-convert-extended-stored-procedure-api.md)  
  
  
