---
title: srv_setutype (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_setutype
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_setutype
ms.assetid: 6160f15d-1b68-411e-ab6d-491ec288f264
author: rothja
ms.author: jroth
ms.openlocfilehash: 70cacca6e6694d914c4b66b7e6eb813b012cf2b3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85755811"
---
# <a name="srv_setutype-extended-stored-procedure-api"></a>srv_setutype (API de procedimento armazenado estendido)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
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
  
## <a name="returns"></a>Retornos  
 SUCCEED ou FAIL. Retornará FAIL se a coluna não existir.  
  
## <a name="remarks"></a>Comentários  
 Uma coluna tem dois tipos de dados: seu tipo de dados real e seu tipo de dados definido pelo usuário. O tipo de dados definido pelo usuário é usado pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar o tipo de dados real definido pelo usuário da coluna, se houver, e informações de descrição de coluna, como a nulidade e a capacidade de atualização, para a coluna.  
  
 A função **srv_setutype** pode ser chamada a qualquer momento em que *column* tenha sido definido com **srv_describe** e antes que a última linha tenha sido enviada.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://www.microsoft.com/msrc?rtc=1).  
  
## <a name="see-also"></a>Consulte Também  
 [srv_describe &#40;API de Procedimento Armazenado Estendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
