---
title: srv_setcoldata (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_setcoldata
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_setcoldata
ms.assetid: 2e19205a-25ca-4d4a-916b-d591cf2c892b
author: rothja
ms.author: jroth
ms.openlocfilehash: 70612b61740c0467de31c01bb5383012ea953aea
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85755824"
---
# <a name="srv_setcoldata-extended-stored-procedure-api"></a>srv_setcoldata (API de procedimento armazenado estendido)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Especifica o endereço atual dos dados de uma coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_setcoldata (  
SRV_PROC *  
srvproc  
,  
int   
column  
,  
void *  
data   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que atua como identificador de uma conexão de cliente específica. A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *column*  
 Indica o número da coluna para a qual o endereço está sendo especificado. As colunas são numeradas a partir de 1.  
  
 *dados*  
 É um ponteiro para os dados de uma coluna. A memória alocada para *data* não deve ser liberada até que os dados da coluna sejam substituídos por outra chamada para **srv_setcoldata**, ou até que **srv_senddone** seja chamado.  
  
## <a name="returns"></a>Retornos  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
 Cada coluna da linha deve ser definida primeiro com **srv_describe**. Os endereços dos dados da coluna são definidos inicialmente com **srv_describe**. Se o endereço dos dados da coluna for alterado, **srv_setcoldata** deverá ser chamado para especificar o novo endereço e **srv_setcoldata** deverá ser chamado separadamente para cada coluna alterada.  
  
 Os dados nulos são representados definindo-se o comprimento da coluna como 0 com **srv_setcollen**. Portanto, o endereço dos dados é ignorado.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte Também  
 [srv_describe &#40;API de Procedimento Armazenado Estendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
