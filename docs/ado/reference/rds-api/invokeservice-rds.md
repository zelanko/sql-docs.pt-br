---
description: InvokeService (RDS)
title: InvokeService (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InvokeService [RDS]
ms.assetid: ad45c676-ec7e-4a3a-9a6b-a54f75eb3012
author: rothja
ms.author: jroth
ms.openlocfilehash: acd5dc5f78319c8fc75891dbaad5a98fc4463196
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88981967"
---
# <a name="invokeservice-rds"></a>InvokeService (RDS)
Retorna um ponteiro para a interface solicitada em uma versão mais compatível do objeto.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o  [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.InvokeService(REFID riid, IUknown* punkNotSoFunctionalInterface, IUknown** ppunkMoreFunctionalInterface) As HRESULT  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *riid*  
  
 no O identificador da interface que está sendo solicitada.  
  
 *punkNotSoFunctionalInterface*  
  
 no O objeto de fonte menos compatível.  
  
 *ppunkMoreFunctionalInterface*  
  
 fora O endereço da variável de ponteiro que recebe o ponteiro de interface solicitado em *riid*. Após o retorno bem-sucedido, o parâmetro *ppunkMoreFunctionalInterface* contém o ponteiro de interface solicitado para o objeto. Se o objeto não oferecer suporte à interface especificada em *riid*, *ppunkMoreFunctionalInterface* será definido como NULL.  
  
## <a name="return-value"></a>Valor de retorno  
 Um valor HRESULT que indica se a chamada para o método **InvokeService** foi bem-sucedida.  
  
## <a name="remarks"></a>Comentários  
 A implementação do mecanismo de cursor do RDS de **InvokeService** usa o conjunto de linhas de entrada (ou um objeto de resultados múltiplos), popula o mecanismo de cursor do conjunto de linhas de entrada e, em seguida, retorna um ponteiro para si mesmo.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Interface IRDSService (RDS)](./irdsservice-interface-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos RDS](./rds-methods.md)