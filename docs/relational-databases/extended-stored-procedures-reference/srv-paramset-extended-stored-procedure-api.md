---
title: srv_paramset (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_paramset
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramset
ms.assetid: 2a509206-a1b8-4b20-b0a2-ef680cef7bd8
author: rothja
ms.author: jroth
ms.openlocfilehash: c3ec0de44aacbcfb2d4e6b96d7525da900017e01
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75253548"
---
# <a name="srv_paramset-extended-stored-procedure-api"></a>srv_paramset (API de procedimento armazenado estendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Define o valor de um parâmetro de retorno de chamada do procedimento armazenado remoto. Esta função foi substituída pela função **srv_paramsetoutput**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_paramset (  
SRV_PROC *  
srvproc  
,  
int  
n  
,   
void *  
data  
,  
int  
len   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que identifica uma conexão de cliente específica (nesse caso, o identificador que recebeu a chamada do procedimento armazenado remoto). A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *n*  
 Indica o número do parâmetro a ser definido. O primeiro parâmetro é 1.  
  
 *dados*  
 É um ponteiro para o valor dos dados a ser enviado de volta ao cliente como o parâmetro de retorno do procedimento armazenado remoto.  
  
 *Len*  
 Especifica o comprimento dos dados a serem retornados. Se o tipo de dados do parâmetro tiver um tamanho constante e não permitir valores nulos (por exemplo, *srvbit* ou *srvint1*), *len* será ignorado.  
  
## <a name="returns"></a>Retornos  
 SUCCEED se o valor do parâmetro tiver sido definido com êxito; caso contrário, FAIL. FAIL será retornado quando não houver procedimentos armazenados remotos atuais, quando não existir o *n*-ésimo parâmetro de procedimento armazenado remoto, quando o parâmetro não for um parâmetro de retorno e quando o argumento *len* não for válido.  
  
 Se *len* for 0, NULL será retornado. Definir *len* como 0 é o único modo de retornar NULL ao cliente.  
  
 Essa função retornará os valores a seguir, se o parâmetro for um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] dos tipos de dados.  
  
|Novos tipos de dados|Comprimento dos dados de retorno|  
|--------------------|------------------------|  
|**BITN**|**NULL:** _len_ = 0, data = IG, RET = 0<br /><br /> **ZERO:** N/A<br /><br /> **>= 255:** N/A<br /><br /> **<255:** N/A|  
|**BIGVARCHAR**|**NULL:** _len_ = 0, data = IG, RET = 1<br /><br /> **ZERO:** _len_ = IG, data = IG, RET = 0<br /><br /> **>=255:** _len_ = max8k, data = valid, RET = 0<br /><br /> **<255:** _len_ = <8k, data = valid, RET = 1|  
|**BIGCHAR**|**NULL:** _len_ = 0, data = IG, RET = 1<br /><br /> **ZERO:** _len_ = IG, data = IG, RET = 0<br /><br /> **>=255:** _len_ = max8k, data = valid, RET = 0<br /><br /> **<255:** _len_ = <8k, data = valid, RET = 1|  
|**BIGBINARY**|**NULL:** _len_ = 0, data = IG, RET = 1<br /><br /> **ZERO:** _len_ = IG, data = IG, RET = 0<br /><br /> **>=255:** _len_ = max8k, data = valid, RET = 0<br /><br /> **<255:** _len_ = <8k, data = valid, RET = 1|  
|**BIGVARBINARY**|**NULL:** _len_ = 0, data = IG, RET = 1<br /><br /> **ZERO:** _len_ = IG, data = IG, RET = 0<br /><br /> **>=255:** _len_ = max8k, data = valid, RET = 0<br /><br /> **<255:** _len_ = <8k, data = valid, RET = 1|  
|NCHAR|**NULL:** _len_ = 0, data = IG, RET = 1<br /><br /> **ZERO:** _len_ = IG, data = IG, RET = 0<br /><br /> **>=255:** _len_ = max8k, data = valid, RET = 0<br /><br /> **<255:** _len_ = <8k, data = valid, RET = 1|  
|NVARCHAR|**NULL:** _len_ = 0, data = IG, RET = 1<br /><br /> **ZERO:** _len_ = IG, data = IG, RET = 0<br /><br /> **>=255:** _len_ = max8k, data = valid, RET = 0<br /><br /> **<255:** _len_ = <8k, data = valid, RET = 1|  
|**NTEXT**|**NULL:** _len_ = IG, data = IG, RET = 0<br /><br /> **ZERO:** _len_ = IG, data = IG, RET = 0<br /><br /> **>=255:** _len_ = IG, data = IG, RET = 0<br /><br /> 255: _Len_ = IG, data = IG, RET = 0 ** \<**|  
|RET = Valor de retorno de srv_paramset||  
|IG = Valor será ignorado||  
|valid = Qualquer ponteiro válido para dados||  
  
## <a name="remarks"></a>Comentários  
 Os parâmetros contêm dados passados entre os clientes e o aplicativo com procedimentos armazenados remotos. O cliente pode especificar certos parâmetros como parâmetros de retorno. Esses parâmetros de retorno podem conter valores que o aplicativo servidor Open Data Services devolve ao cliente. Usar parâmetros de retorno equivale a passar parâmetros por referência.  
  
 Você não pode definir o valor de retorno para um parâmetro que não foi invocado como um parâmetro de retorno. Use **srv_paramstatus** para determinar como o parâmetro foi invocado.  
  
 Esta função define o valor de retorno para um parâmetro, mas não envia o valor de retorno ao cliente. Todos os parâmetros de retorno, independentemente se seus valores retornados foram ou não com **srv_paramset**, serão automaticamente enviados ao cliente quando **srv_senddone** for chamado com o sinalizador de status SRV_DONE_FINAL definido.  
  
 Quando uma chamada de procedimento armazenado remoto é feita com parâmetros, os parâmetros podem ser passados pelo nome ou pela posição (sem-nome). Se a chamada de procedimento armazenado remoto for feita com alguns parâmetros transmitidos pelo nome e outros pela posição, ocorrerá um erro. O manipulador SRV_RPC ainda é chamado, mas aparece como se não houvesse parâmetros e **srv_rpcparams** retorna 0.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://www.microsoft.com/msrc?rtc=1).  
  
## <a name="see-also"></a>Consulte Também  
 [srv_paramsetoutput &#40;API de Procedimento Armazenado Estendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-paramsetoutput-extended-stored-procedure-api.md)  
  
  
