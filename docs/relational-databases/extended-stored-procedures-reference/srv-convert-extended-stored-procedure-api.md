---
title: srv_convert (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- srv_convert
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_convert
ms.assetid: 216b4a31-786e-4361-8a33-e5f6e9790f90
caps.latest.revision: 33
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1feb6b6071958b6bbf73bcb2b50d785dffc1a87e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="srvconvert-extended-stored-procedure-api"></a>srv_convert (API de procedimento armazenado estendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Altera dados de um tipo de dados para outro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_convert (  
SRV_PROC *  
srvproc  
,  
int  
srctype  
,  
void *  
src  
,  
DBINT  
srclen  
,  
int  
desttype  
,  
void *  
  dest  
,  
DBINT  
destlen  
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que atua como identificador de uma conexão de cliente específica. A estrutura contém todas as informações de controle que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar as comunicações e os dados entre o aplicativo e o cliente. Caso o identificador *srvproc* seja fornecido, ele será passado para a função de manipulador de erro da API de Procedimento Armazenado Estendido quando ocorrer um erro.  
  
 *srctype*  
 Especifica o tipo de dados dos dados a serem convertidos. Este parâmetro pode ser qualquer um dos tipos de dados da API de procedimento armazenado estendido.  
  
 *src*  
 Trata-se de um ponteiro para os dados a serem convertidos. Este parâmetro pode ser qualquer um dos tipos de dados da API de procedimento armazenado estendido.  
  
 *srclen*  
 Especifica o comprimento, em bytes, dos dados a serem convertidos. Caso *srclen* seja 0, **srv_convert** colocará um valor nulo na variável de destino. A menos que seja 0, esse parâmetro é ignorado para tipos de dados com comprimento fixo, quando se pressupõe que os dados sejam NULL. Para dados do tipo de dados SRVCHAR, um comprimento igual a -1 indica a cadeia de caracteres é terminada em nulo.  
  
 *desttype*  
 Especifica o tipo de dados no qual converter a origem. Este parâmetro pode ser qualquer um dos tipos de dados da API de procedimento armazenado estendido.  
  
 *dest*  
 Trata-se de um ponteiro para a variável de destino que recebe dados convertidos. Caso esse ponteiro seja NULL, **srv_convert** chamará o manipulador de erro fornecido pelo usuário, se houver, e retornará -1.  
  
 Caso *desttype* seja SRVDECIMAL ou SRVNUMERIC, o parâmetro *dest* deverá ser um ponteiro para uma estrutura DBNUMERIC ou DBDECIMAL com os campos de precisão e escala da estrutura já definidos com os valores desejados. É possível usar DEFAULTPRECISION para especificar uma precisão padrão, e DEFAULTSCALE para especificar uma escala padrão.  
  
 *destlen*  
 Especifica o comprimento, em bytes, da variável de destino. Esse parâmetro é ignorado para tipos de dados com comprimento fixo. Para uma variável de destino do tipo SRVCHAR, o valor igual a *destlen* deve ser o tamanho total do espaço do buffer de destino. Um comprimento igual a -1 para uma variável de destino do tipo SRVCHAR ou SRVBINARY indica se há espaço suficiente disponível. Para uma variável de destino do tipo *srvchar*, um tamanho igual a -1 faz com que a cadeia de caracteres termine em nulo.  
  
## <a name="returns"></a>Retorna  
 O comprimento dos dados convertidos, em bytes, caso a conversão do tipo de dados tenha êxito. Quando **srv_convert** encontra uma solicitação para uma conversão para a qual não dá suporte, ele chama o manipulador de erro fornecido pelo desenvolvedor, se houver, define um número de erro global e retorna -1.  
  
## <a name="remarks"></a>Remarks  
 A função **srv_willconvert** determina se uma conversão específica é permitida.  
  
 A conversão para os tipos de dados numéricos aproximados SRVFLT4 ou SRVFLT8 pode resultar em uma certa perda de precisão. A conversão dos tipos de dados numéricos aproximados SRVFLT4 ou SRVFLT8 em SRVCHAR ou SRVTEXT também pode resultar em alguma perda de precisão.  
  
 A conversão em SRVFLT*x*, SRVINT*x*, SRVMONEY, SRVMONEY4, SRVDECIMAL ou SRVNUMERIC pode resultar em estouro, caso o número seja maior que o valor máximo do destino ou em estouro negativo, caso o número seja menor que o valor mínimo do destino. Caso o estouro ocorra durante a conversão em SRVCHAR ou SRVTEXT, o primeiro caractere do valor resultante contém um asterisco (*) para indicar o erro.  
  
 Ao converter SRVCHAR em SRVBINARY, **srv_convert** interpreta SRVCHAR como hexadecimal, independentemente da cadeia de caracteres conter um 0 à esquerda. Ao converter SRVBINARY em SRVCHAR, **srv_convert** cria uma cadeia de caracteres hexadecimal sem um 0 à esquerda. Em todos os demais casos, uma conversão para ou do tipo de dados SRVBINARY é uma cópia de bit direta.  
  
 Em determinados casos, isso pode ser útil na conversão de um tipo de dados em si mesmo. Por exemplo, a conversão de SRVCHAR em SRVCHAR com *destlen* igual -1 adiciona um terminador nulo a uma cadeia de caracteres.  
  
 Para obter uma descrição dos tipos de dados e das conversões de tipo de dados da API de Procedimento Armazenado Estendido, consulte [Tipos de dados &#40;API de Procedimento Armazenado Estendido&#41;](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md).  
  
 A função **srv_convert** pode falhar por várias razões:  
  
-   A conversão solicitada não está disponível.  
  
-   A conversão resultou em truncamento, estouro ou perda de precisão na variável de destino.  
  
-   Ocorreu um erro de sintaxe durante a conversão de uma cadeia de caracteres em um tipo de dados numérico.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte também  
 [srv_setutype &#40;API de Procedimento Armazenado Estendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-setutype-extended-stored-procedure-api.md)   
 [srv_willconvert &#40;API de Procedimento Armazenado Estendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-willconvert-extended-stored-procedure-api.md)  
  
  
