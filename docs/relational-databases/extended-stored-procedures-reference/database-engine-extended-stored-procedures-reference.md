---
title: Referência do programador de procedimentos armazenados estendidos | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], listed
ms.assetid: 4e9d0374-0927-4f17-bab9-2215b1b8fea8
author: rothja
ms.author: jroth
ms.openlocfilehash: 61755c4b360332042721ccd7ec9213a727ee4ad9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85679099"
---
# <a name="database-engine-extended-stored-procedures---reference"></a>Procedimento armazenado estendido do Mecanismo de Banco de Dados – referência
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 A [!INCLUDE[msCoName](../../includes/msconame-md.md)] API de procedimento armazenado estendido, anteriormente parte do Open Data Services, fornece uma API (interface de programação de aplicativo) baseada em servidor para estender a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funcionalidade. A API consiste nas funções e macros C e C++ usadas para criar aplicativos.  
  
 Com o surgimento de tecnologias mais novas e mais avançadas, como a integração CLR, a necessidade de procedimentos armazenados estendidos foi amplamente substituída.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|||  
|-|-|  
|[Tipos de dados](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md)|[srv_pfield](../../relational-databases/extended-stored-procedures-reference/srv-pfield-extended-stored-procedure-api.md)|  
|[srv_alloc](../../relational-databases/extended-stored-procedures-reference/srv-alloc-extended-stored-procedure-api.md)||  
|[srv_convert](../../relational-databases/extended-stored-procedures-reference/srv-convert-extended-stored-procedure-api.md)|[srv_pfieldex](../../relational-databases/extended-stored-procedures-reference/srv-pfieldex-extended-stored-procedure-api.md)|  
|[srv_describe](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)|[srv_rpcdb](../../relational-databases/extended-stored-procedures-reference/srv-rpcdb-extended-stored-procedure-api.md)|  
|[srv_getbindtoken](../../relational-databases/extended-stored-procedures-reference/srv-getbindtoken-extended-stored-procedure-api.md)|[srv_rpcname](../../relational-databases/extended-stored-procedures-reference/srv-rpcname-extended-stored-procedure-api.md)|  
|[srv_got_attention](../../relational-databases/extended-stored-procedures-reference/srv-got-attention-extended-stored-procedure-api.md)|[srv_rpcnumber](../../relational-databases/extended-stored-procedures-reference/srv-rpcnumber-extended-stored-procedure-api.md)|  
||[srv_rpcoptions](../../relational-databases/extended-stored-procedures-reference/srv-rpcoptions-extended-stored-procedure-api.md)|  
|[srv_message_handler](../../relational-databases/extended-stored-procedures-reference/srv-message-handler-extended-stored-procedure-api.md)|[srv_rpcowner](../../relational-databases/extended-stored-procedures-reference/srv-rpcowner-extended-stored-procedure-api.md)|  
|[srv_paramdata](../../relational-databases/extended-stored-procedures-reference/srv-paramdata-extended-stored-procedure-api.md)|[srv_rpcparams](../../relational-databases/extended-stored-procedures-reference/srv-rpcparams-extended-stored-procedure-api.md)|  
|[srv_paraminfo](../../relational-databases/extended-stored-procedures-reference/srv-paraminfo-extended-stored-procedure-api.md)|[srv_senddone](../../relational-databases/extended-stored-procedures-reference/srv-senddone-extended-stored-procedure-api.md)|  
|[srv_paramlen](../../relational-databases/extended-stored-procedures-reference/srv-paramlen-extended-stored-procedure-api.md)|[srv_sendmsg](../../relational-databases/extended-stored-procedures-reference/srv-sendmsg-extended-stored-procedure-api.md)|  
|[srv_parammaxlen](../../relational-databases/extended-stored-procedures-reference/srv-parammaxlen-extended-stored-procedure-api.md)|[srv_sendrow](../../relational-databases/extended-stored-procedures-reference/srv-sendrow-extended-stored-procedure-api.md)|  
|[srv_paramname](../../relational-databases/extended-stored-procedures-reference/srv-paramname-extended-stored-procedure-api.md)|[srv_setcoldata](../../relational-databases/extended-stored-procedures-reference/srv-setcoldata-extended-stored-procedure-api.md)|  
|[srv_paramnumber](../../relational-databases/extended-stored-procedures-reference/srv-paramnumber-extended-stored-procedure-api.md)|[srv_setcollen](../../relational-databases/extended-stored-procedures-reference/srv-setcollen-extended-stored-procedure-api.md)|  
|[srv_paramset](../../relational-databases/extended-stored-procedures-reference/srv-paramset-extended-stored-procedure-api.md)|[srv_setutype](../../relational-databases/extended-stored-procedures-reference/srv-setutype-extended-stored-procedure-api.md)|  
|[srv_paramsetoutput](../../relational-databases/extended-stored-procedures-reference/srv-paramsetoutput-extended-stored-procedure-api.md)|[srv_willconvert](../../relational-databases/extended-stored-procedures-reference/srv-willconvert-extended-stored-procedure-api.md)|  
|[srv_paramstatus](../../relational-databases/extended-stored-procedures-reference/srv-paramstatus-extended-stored-procedure-api.md)|[srv_wsendmsg](../../relational-databases/extended-stored-procedures-reference/srv-wsendmsg-extended-stored-procedure-api.md)|  
|[srv_paramtype](../../relational-databases/extended-stored-procedures-reference/srv-paramtype-extended-stored-procedure-api.md)||  
  
  
