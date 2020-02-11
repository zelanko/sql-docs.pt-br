---
title: srv_paraminfo (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paraminfo
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paraminfo
ms.assetid: ee2afd4e-0d91-462b-9403-98d481546330
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f3c89eb2e6f810902e28e01c7e5ffbcdcc0375c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63127183"
---
# <a name="srv_paraminfo-extended-stored-procedure-api"></a>srv_paraminfo (API de procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Em vez disso, use a integração CLR.  
  
 Retorna informações sobre um parâmetro. Essa função substitui as seguintes funções: [srv_paramtype](srv-paramtype-extended-stored-procedure-api.md), [srv_paramlen](srv-paramlen-extended-stored-procedure-api.md), [srv_parammaxlen](srv-parammaxlen-extended-stored-procedure-api.md) e [srv_paramdata](srv-paramdata-extended-stored-procedure-api.md). o **srv_paraminfo** dá suporte aos tipos de dados em [tipos de dados](data-types-extended-stored-procedure-api.md) e dados de comprimento zero.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_paraminfo (  
SRV_PROC *  
srvproc  
,  
int  
n  
,  
BYTE *  
pbType  
,  
ULONG *  
pcbMaxLen  
,  
ULONG *  
pcbActualLen  
,  
BYTE *  
pbData  
,  
BOOL *  
pfNull  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Um identificador para uma conexão do cliente.  
  
 *n*  
 O número ordinal do parâmetro para ser definido. O primeiro parâmetro é 1.  
  
 *pbType*  
 O tipo de dados do parâmetro.  
  
 *pcbMaxLen*  
 Ponteiro para o comprimento máximo do parâmetro.  
  
 *pcbActualLen*  
 Ponteiro para o comprimento real do parâmetro. Um valor igual a 0 (\**pcbActualLen* == 0) significa dados de comprimento zero se **pfNull* está definida como FALSE.  
  
 *pbData*  
 Ponteiro para o buffer para obter dados de parâmetro. Se *pbData* não for NULL, a API de Procedimento Armazenado Estendido gravará \**pcbActualLen* bytes de dados em \**pbData*. Se *pbData* for NULL, nenhum dado será gravado em \**pbData*, mas a função retorna \**pbType*, \**pcbMaxLen*, \**pcbActualLen* e **pfNull*. A memória para este buffer deve ser gerenciada pelo aplicativo.  
  
 *pfNull*  
 Ponteiro para um sinalizador nulo. **pfNull* será definido como true se o valor do parâmetro for NULL.  
  
## <a name="returns"></a>Retornos  
 Se a informações de parâmetro tiverem sido obtidas com êxito, SUCCEED será retornado. Caso contrário, o retorno será FAIL. FAIL será retornado quando não houver procedimento armazenado remoto atual e quando não houver parâmetro para o *n*-ésimo procedimento armazenado remoto.  
  
## <a name="remarks"></a>Comentários  
 **Observação de segurança** Você deve examinar detalhadamente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do programador de procedimentos armazenados estendidos](database-engine-extended-stored-procedures-reference.md)  
  
  
