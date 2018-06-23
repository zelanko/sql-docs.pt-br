---
title: Referência do programador de procedimentos armazenados estendidos | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- extended stored procedures [SQL Server], listed
ms.assetid: 4e9d0374-0927-4f17-bab9-2215b1b8fea8
caps.latest.revision: 38
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8fa79d3dbfe487ab46b374d0e5a7aed85bcb2a60
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012257"
---
# <a name="extended-stored-procedures-programmer39s-reference"></a>Estendido programador de procedimentos armazenados&#39;s referência
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 A API de Procedimento Armazenado Estendido da [!INCLUDE[msCoName](../../includes/msconame-md.md)], anteriormente parte do Open Data Services, fornece uma API (interface de programação de aplicativo) baseada em servidor para estender a funcionalidade do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A API consiste nas funções e macros C e C++ usadas para criar aplicativos.  
  
 Com o surgimento de tecnologias mais novas e mais avançadas, como a integração CLR, a necessidade de procedimentos armazenados estendidos foi amplamente substituída.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|||  
|-|-|  
|[Tipos de Dados](srv-pfield-extended-stored-procedure-api.md)|  
|[srv_alloc](srv-alloc-extended-stored-procedure-api.md)||  
|[srv_convert](srv-pfieldex-extended-stored-procedure-api.md)|  
|[srv_describe](srv-rpcdb-extended-stored-procedure-api.md)|  
|[srv_getbindtoken](srv-rpcname-extended-stored-procedure-api.md)|  
|[srv_got_attention](srv-rpcnumber-extended-stored-procedure-api.md)|  
||[srv_rpcoptions](srv-rpcoptions-extended-stored-procedure-api.md)|  
|[srv_message_handler](srv-rpcowner-extended-stored-procedure-api.md)|  
|[srv_paramdata](srv-rpcparams-extended-stored-procedure-api.md)|  
|[srv_paraminfo](srv-senddone-extended-stored-procedure-api.md)|  
|[srv_paramlen](srv-sendmsg-extended-stored-procedure-api.md)|  
|[srv_parammaxlen](srv-sendrow-extended-stored-procedure-api.md)|  
|[srv_paramname](srv-setcoldata-extended-stored-procedure-api.md)|  
|[srv_paramnumber](srv-setcollen-extended-stored-procedure-api.md)|  
|[srv_paramset](srv-setutype-extended-stored-procedure-api.md)|  
|[srv_paramsetoutput](srv-willconvert-extended-stored-procedure-api.md)|  
|[srv_paramstatus](srv-wsendmsg-extended-stored-procedure-api.md)|  
|[srv_paramtype](srv-paramtype-extended-stored-procedure-api.md)||  
  
  