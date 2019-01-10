---
title: srv_paramlen (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramlen
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramlen
ms.assetid: d1fe92ff-cad6-4396-8216-125e5642e81e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2c858d0fa8579aff288efd7026ab4b65035bad8d
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53364698"
---
# <a name="srvparamlen-extended-stored-procedure-api"></a>srv_paramlen (API de procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Retorna o comprimento de dados de um parâmetro de chamada de procedimento armazenado remoto. Essa função foi substituída pela função **srv_paraminfo**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_paramlen (  
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
 O comprimento real, em bytes, dos dados do parâmetro. Se não houver *n*-ésimo parâmetro nem procedimento armazenado remoto, o valor retornado será -1. Se o *n*-ésimo parâmetro for NULL, retornará 0.  
  
 Essa função retornará os seguintes valores se o parâmetro for um dos tipos de dados a seguir do sistema do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
|Novos tipos de dados|Comprimento dos dados de entrada|  
|--------------------|-----------------------|  
|`BITN`|**NULL:** 1<br /><br /> **ZERO:** 1<br /><br /> **> = 255:** N/D<br /><br /> **< 255:** N/D|  
|`BIGVARCHAR`|**NULL:** 0<br /><br /> **ZERO:** 1<br /><br /> **> = 255:** 255<br /><br /> **<255:** *len* real|  
|`BIGCHAR`|**NULL:** 0<br /><br /> **ZERO:** 255<br /><br /> **> = 255:** 255<br /><br /> **< 255:** 255|  
|`BIGBINARY`|**NULL:** 0<br /><br /> **ZERO:** 255<br /><br /> **> = 255:** 255<br /><br /> **< 255:** 255|  
|`BIGVARBINARY`|**NULL:** 0<br /><br /> **ZERO:** 1<br /><br /> **> = 255:** 255<br /><br /> **<255:** *len* real|  
|`NCHAR`|**NULL:** 0<br /><br /> **ZERO:** 255<br /><br /> **> = 255:** 255<br /><br /> **< 255:** 255|  
|`NVARCHAR`|**NULL:** 0<br /><br /> **ZERO:** 1<br /><br /> **> = 255:** 255<br /><br /> **<255:** *len* real|  
|`NTEXT`|**NULL:** -1<br /><br /> **ZERO:** -1<br /><br /> **>=255:** -1<br /><br /> **< 255:** -1|  
  
 \*   *len* real = tamanho da cadeia de caracteres de vários bytes (cch)  
  
## <a name="remarks"></a>Comentários  
 Cada parâmetro de procedimento armazenado remoto tem um comprimento de dados real e um máximo. Para tipos de dados padrão de comprimento fixo que não permitem valores nulos, os comprimentos real e máximo são os mesmos. Para tipos de dados de comprimento de variável, os comprimentos podem variar. Por exemplo, um parâmetro declarado como `varchar(30)` pode ter dados de apenas 10 bytes de comprimento. O comprimento real do parâmetro é 10 e seu comprimento máximo é 30. A função **srv_paramlen** obtém o tamanho real de dados, em bytes, de um procedimento armazenado remoto. Para obter o tamanho máximo de dados de um parâmetro, use **srv_parammaxlen**.  
  
 Quando uma chamada de procedimento armazenado remoto é feita com parâmetros, os parâmetros podem ser passados pelo nome ou pela posição (sem-nome). Se a chamada de procedimento armazenado remoto for feita com alguns parâmetros transmitidos pelo nome e outros pela posição, ocorrerá um erro. O manipulador SRV_RPC ainda O manipulador SRV_RPC ainda é chamado, mas aparece como se não houvesse parâmetros e **srv_rpcparams** retorna 0.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte também  
 [srv_paraminfo &#40;API de Procedimento Armazenado Estendido&#41;](srv-paraminfo-extended-stored-procedure-api.md)   
 [srv_rpcparams &#40;API de Procedimento Armazenado Estendido&#41;](srv-rpcparams-extended-stored-procedure-api.md)  
  
  
