---
title: srv_setutype (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_setutype
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_setutype
ms.assetid: 6160f15d-1b68-411e-ab6d-491ec288f264
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2439b19c4550d07b8d50a0bed6d72b603b1601a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62745785"
---
# <a name="srvsetutype-extended-stored-procedure-api"></a>srv_setutype (API de procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Define o tipo de dados definido pelo usuário para uma coluna em uma linha.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_setutype (  
SRV_PROC *  
srvproc  
,  
int   
column  
,   
DBINT  
user_type   
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que atua como identificador de uma conexão de cliente específica. A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *column*  
 Indica qual coluna deve ser definida. As colunas são numeradas a partir de 1.  
  
 *user_type*  
 Especifica o código do tipo de dados definido pelo usuário.  
  
## <a name="returns"></a>Retorna  
 SUCCEED ou FAIL. Retornará FAIL se a coluna não existir.  
  
## <a name="remarks"></a>Comentários  
 Uma coluna tem dois tipos de dados: seu tipo de dados real e seu tipo de dados definido pelo usuário. O tipo de dados definido pelo usuário é usado pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar o tipo de dados definido pelo usuário real da coluna, se houver, e as informações de descrição da coluna, como sua nulidade e sua capacidade de atualização.  
  
 A função **srv_setutype** pode ser chamada a qualquer momento em que *column* tenha sido definido com **srv_describe** e antes que a última linha tenha sido enviada.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte também  
 [srv_describe &#40;API de Procedimento Armazenado Estendido&#41;](srv-describe-extended-stored-procedure-api.md)  
  
  
