---
title: srv_paraminfo (API de Procedimento Armazenado Estendido) | Microsoft Docs
description: Saiba como srv_paraminfo na API de procedimento armazenado estendido retorna informações sobre um parâmetro.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_paraminfo
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paraminfo
ms.assetid: ee2afd4e-0d91-462b-9403-98d481546330
author: rothja
ms.author: jroth
ms.openlocfilehash: 78057c092942455e41f48e0f9f12a9502c1a67ee
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87332327"
---
# <a name="srv_paraminfo-extended-stored-procedure-api"></a>srv_paraminfo (API de procedimento armazenado estendido)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Retorna informações sobre um parâmetro. Essa função substitui as seguintes funções: [srv_paramtype](../../relational-databases/extended-stored-procedures-reference/srv-paramtype-extended-stored-procedure-api.md), [srv_paramlen](../../relational-databases/extended-stored-procedures-reference/srv-paramlen-extended-stored-procedure-api.md), [srv_parammaxlen](../../relational-databases/extended-stored-procedures-reference/srv-parammaxlen-extended-stored-procedure-api.md) e [srv_paramdata](../../relational-databases/extended-stored-procedures-reference/srv-paramdata-extended-stored-procedure-api.md). **srv_paraminfo** dá suporte aos tipos de dados em [Tipos de Dados](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md) e dados de comprimento zero.  
  
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
 Ponteiro para um sinalizador nulo. **pfNull* será definido como TRUE se o valor do parâmetro for NULL.  
  
## <a name="returns"></a>Retornos  
 Se a informações de parâmetro tiverem sido obtidas com êxito, SUCCEED será retornado. Caso contrário, o retorno será FAIL. FAIL será retornado quando não houver procedimento armazenado remoto atual e quando não houver parâmetro para o *n*-ésimo procedimento armazenado remoto.  
  
## <a name="remarks"></a>Comentários  
 **Observação de segurança** Você deve examinar detalhadamente o código-fonte de procedimentos armazenados estendidos e testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do programador de procedimentos armazenados estendidos](../../relational-databases/extended-stored-procedures-reference/database-engine-extended-stored-procedures-reference.md)  
  
  
