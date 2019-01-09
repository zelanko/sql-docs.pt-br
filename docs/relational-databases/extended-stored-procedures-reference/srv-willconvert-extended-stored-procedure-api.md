---
title: srv_willconvert (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e091dded3b9c763be6d5d891ac7026146feb0a0d
ms.sourcegitcommit: edf7372cb674179f03a330de5e674824a8b4118f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53246655"
---
# <a name="srvwillconvert-extended-stored-procedure-api"></a>srv_willconvert (API de procedimento armazenado estendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
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
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://www.microsoft.com/en-us/msrc?rtc=1).  
  
## <a name="see-also"></a>Consulte Também  
 [srv_convert &#40;API de Procedimento Armazenado Estendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-convert-extended-stored-procedure-api.md)  
  
  
