---
title: srv_pfieldex (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- srv_pfieldex
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_pfieldex
ms.assetid: d4e9a34b-b3a3-434f-8556-768bd20d145a
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c885847e046e17963f6d21e1615f0fb2dad4c85d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48187516"
---
# <a name="srvpfieldex-extended-stored-procedure-api"></a>srv_pfieldex (API de procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Retorna um ponteiro para dados que contêm o campo SRV_PROC solicitado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
void *srv_pfieldex(SRV_PROC *   
srvproc  
, int   
field  
, int *   
len  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que atua como identificador de uma conexão de cliente específica. A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *field*  
 Especifica o campo *srvproc* a ser retornado.  
  
|Campo|Description|Tipo de retorno|  
|-----------|-----------------|------------------|  
|SRV_MSGLCID|LCID de mensagem da sessão atual.|ULONG *|  
|SRV_INSTANCENAME|Nome de instância (se nomeado); caso contrário, retorna NULL.|WCHAR*|  
  
 *len*  
 É um ponteiro para uma variável **int** que contém o tamanho do valor de *field* retornado, em bytes. Se *len* for NULL, o tamanho não será retornado. Quando NULL é retornado, **len* é definido como 0.  
  
## <a name="returns"></a>Retorna  
 Um ponteiro para dados cujo tipo depende de *field*. NULL é retornado quando *len* é NULL ou *srvproc* é NULL. Se o *field* for desconhecido, NULL será retornado. Quando NULL é retornado, **len* é definido como 0.  
  
> [!IMPORTANT]  
>  O buffer retornado pelo servidor deve ser somente leitura. Caso contrário, o estado do servidor pode estar corrompido.  
  
## <a name="remarks"></a>Comentários  
 **Observação de segurança** Você deve examinar detalhadamente o código-fonte de procedimentos armazenados estendidos e testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  
