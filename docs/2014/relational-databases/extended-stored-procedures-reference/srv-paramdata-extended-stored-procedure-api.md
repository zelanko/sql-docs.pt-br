---
title: srv_paramdata (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramdata
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramdata
ms.assetid: 3104514d-b404-47c9-b6d7-928106384874
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0825b86cabf57df552063335a0870461cb8a5658
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63127417"
---
# <a name="srv_paramdata-extended-stored-procedure-api"></a>srv_paramdata (API de procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Em vez disso, use a integração CLR.  
  
 Retorna o valor de um parâmetro de chamada de procedimento armazenado remoto. Essa função foi substituída pela função **srv_paraminfo**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
void * srv_paramdata (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que identifica uma conexão de cliente específica (nesse caso, o identificador que recebeu a chamada do procedimento armazenado remoto). A estrutura contém informações que a biblioteca do procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *n*  
 É o número do parâmetro. O primeiro parâmetro equivale ao número 1.  
  
## <a name="returns"></a>Retornos  
 Um ponteiro para o valor do parâmetro. Se o *n*-ésimo parâmetro for NULL, se não houver *n*-ésimo parâmetro ou não houver procedimento armazenado remoto, retornará NULL. Se o valor do parâmetro for uma cadeia de caracteres, ele não pode terminar com caractere nulo. Use **srv_paramlen** para determinar o tamanho da cadeia de caracteres.  
  
 Essa função retornará os valores a seguir, se o parâmetro for um dos [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados. Os dados de ponteiro indicam se o ponteiro para o tipo de dados é válido (VP), NULL ou não aplicável (N/A) e o conteúdo dos dados apontados.  
  
|Novos tipos de dados|Comprimento dos dados de entrada|  
|--------------------|-----------------------|  
|BITN|**Nulo:** VP, NULO<br /><br /> **Zero:** VP, NULO<br /><br /> **>= 255:** N/A<br /><br /> **<255:** N/A|  
|BIGVARCHAR|**Nulo:** NULL, N/A<br /><br /> **Zero:** VP, NULO<br /><br /> **>= 255:** VP, 255 caracteres<br /><br /> **<255:** VP, dados reais|  
|BIGCHAR|**Nulo:** NULL, N/A<br /><br /> **Zero:** VP, 255 espaços<br /><br /> **>= 255:** VP, 255 caracteres<br /><br /> **<255:** VP, dados reais + preenchimento (até 255)|  
|BIGBINARY|**Nulo:** NULL, N/A<br /><br /> **Zero:** VP, 255 0x00<br /><br /> **>= 255:** VP, 255 bytes<br /><br /> **<255:** VP, dados reais + preenchimento (até 255)|  
|BIGVARBINARY|**Nulo:** NULL, N/A<br /><br /> **Zero:** VP, 0x00<br /><br /> **>= 255:** VP, 255 bytes<br /><br /> **<255:** VP, dados reais|  
|NCHAR|**Nulo:** NULL, N/A<br /><br /> **Zero:** VP, 255 espaços<br /><br /> **>= 255:** VP, 255 caracteres<br /><br /> **<255:** VP, dados reais + preenchimento (até 255)|  
|NVARCHAR|**Nulo:** NULL, N/A<br /><br /> **Zero:** VP, NULO<br /><br /> **>= 255:** VP, 255 caracteres<br /><br /> **<255:** VP, dados reais|  
|NTEXT|**Nulo:** N/A<br /><br /> **Zero:** N/A<br /><br /> **>= 255:** N/A<br /><br /> ** \<255:** N/A|  
  
 
  \* Os dados não terminam em nulo; nenhum aviso é emitido no truncamento de dados >255 caracteres.  
  
## <a name="remarks"></a>Comentários  
 Se você souber o nome do parâmetro, poderá usar **srv_paramnumber** para obter o número do parâmetro. Para determinar se um parâmetro é NULL, use **srv_paramlen**.  
  
 Quando uma chamada de procedimento armazenado remoto for feita com parâmetros, os parâmetros poderão ser passados pelo nome ou pela posição (sem-nome). Se a chamada de procedimento armazenado remoto for feita com alguns parâmetros transmitidos pelo nome e outros pela posição, ocorrerá um erro. Em caso de erro, o manipulador SRV_RPC ainda será chamado, mas aparecerá como se não houvesse parâmetros e **srv_rpcparams** retornará 0.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte Também  
 [srv_rpcparams &#40;API de procedimento armazenado estendido&#41;](srv-rpcparams-extended-stored-procedure-api.md)  
  
  
