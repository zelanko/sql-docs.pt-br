---
title: srv_paramtype (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- srv_paramtype
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramtype
ms.assetid: badc6d36-8a87-42b5-b28c-9c4f5ded8552
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 97ecfcb6060ac94424bf42e54fa80bc7e11d5ad1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120357"
---
# <a name="srvparamtype-extended-stored-procedure-api"></a>srv_paramtype (API de procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Retorna o tipo de dados de um parâmetro de chamada de procedimento armazenado remoto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_paramtype (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que identifica uma conexão de cliente específica (nesse caso, o identificador que recebeu a chamada do procedimento armazenado remoto). A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *n*  
 Indica o número do parâmetro. O primeiro parâmetro é 1.  
  
## <a name="returns"></a>Retorna  
 Um valor de token para o tipo de dados do parâmetro. Para obter informações sobre tipos de dados, consulte [Tipos de dados &#40;API de Procedimento Armazenado Estendido&#41;](data-types-extended-stored-procedure-api.md). Se não houver *n*-ésimo parâmetro nem procedimento armazenado remoto, o valor retornado será -1.  
  
 Essa função retornará os valores a seguir se o parâmetro for um dos tipos de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
|Novos tipos de dados|Valor retornado|  
|--------------------|------------------|  
|`BITN`|SRVBIT|  
|`BIGVARCHAR`|VARCHAR|  
|`BIGCHAR`|CHAR|  
|`BIGBINARY`|BINARY|  
|`BIGVARBINARY`|VARBINARY|  
|`NCHAR`|CHAR|  
|`NVARCHAR`|VARCHAR|  
|`NTEXT`|-1|  
  
## <a name="remarks"></a>Remarks  
 Quando uma chamada de procedimento armazenado remoto é feita com parâmetros, os parâmetros podem ser passados pelo nome ou pela posição (sem-nome). Se a chamada de procedimento armazenado remoto for feita com alguns parâmetros transmitidos pelo nome e outros pela posição, ocorrerá um erro. O manipulador SRV_RPC ainda O manipulador SRV_RPC ainda é chamado, mas aparece como se não houvesse parâmetros e **srv_rpcparams** retorna 0.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte também  
 [srv_paraminfo &#40;API de Procedimento Armazenado Estendido&#41;](srv-paraminfo-extended-stored-procedure-api.md)   
 [srv_rpcparams &#40;API de Procedimento Armazenado Estendido&#41;](srv-rpcparams-extended-stored-procedure-api.md)  
  
  