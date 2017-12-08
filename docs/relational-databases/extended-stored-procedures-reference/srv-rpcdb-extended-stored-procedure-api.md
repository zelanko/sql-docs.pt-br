---
title: srv_rpcdb (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: srv_rpcdb
apilocation: opends60.dll
apitype: DLLExport
dev_langs: C++
helpviewer_keywords: srv_rpcdb
ms.assetid: d52bfd22-7a7c-4ab0-af65-df96ff359e6f
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4e83c5a69d87fb61744af1f6f3f2bd44f49be2b3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="srvrpcdb-extended-stored-procedure-api"></a>srv_rpcdb (API do procedimento armazenado estendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Retorna o componente de nome de banco de dados para o procedimento armazenado remoto atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DBCHAR * srv_rpcdb (  
SRV_PROC * srvproc,int *len );  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que atua como identificador de uma conexão de cliente específica. A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *len*  
 É um ponteiro para uma variável **int** que recebe o tamanho do nome do banco de dados. Se *len* for NULL, o tamanho do nome do banco de dados não será retornado.  
  
## <a name="returns"></a>Retorna  
 Um ponteiro DBCHAR para a cadeia de caracteres com terminação nula para a parte do nome do banco de dados do procedimento armazenado remoto atual. Se não houver nenhum procedimento armazenado remoto atual, NULL será retornado e o parâmetro *len* será definido como -1.  
  
## <a name="remarks"></a>Comentários  
 Esta função retorna somente o componente de banco de dados do nome de objeto de procedimento armazenado remoto. Isto não inclui os especificadores opcionais para proprietário, nome do procedimento armazenado remoto e número do procedimento armazenado remoto.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  
