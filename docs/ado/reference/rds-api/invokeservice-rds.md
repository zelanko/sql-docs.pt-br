---
title: InvokeService (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InvokeService [RDS]
ms.assetid: ad45c676-ec7e-4a3a-9a6b-a54f75eb3012
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d7d0c205b5045f4cd743776894f62fbc4f0750cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712647"
---
# <a name="invokeservice-rds"></a>InvokeService (RDS)
Retorna um ponteiro para a interface solicitada em uma versão mais robustos do objeto.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.InvokeService(REFID riid, IUknown* punkNotSoFunctionalInterface, IUknown** ppunkMoreFunctionalInterface) As HRESULT  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *riid*  
  
 [in] O identificador da interface que está sendo solicitado.  
  
 *punkNotSoFunctionalInterface*  
  
 [in] O objeto de origem com menor capacidade.  
  
 *ppunkMoreFunctionalInterface*  
  
 [out] O endereço da variável de ponteiro que recebe o ponteiro de interface solicitado no *riid*. No retorno bem-sucedido, o *ppunkMoreFunctionalInterface* parâmetro contém o ponteiro de interface solicitada para o objeto. Se o objeto não dá suporte a interface especificada na *riid*, *ppunkMoreFunctionalInterface* é definido como NULL.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor HRESULT que indica se a chamada para o **InvokeService** método foi bem-sucedida.  
  
## <a name="remarks"></a>Comentários  
 A implementação do mecanismo de cursor RDS do **InvokeService** usa o conjunto de linhas de entrada (ou o objeto de vários resultados), preenche o mecanismo de cursor do conjunto de linhas de entrada e, em seguida, retorna um ponteiro em si mesmo.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Interface IRDSService (RDS)](../../../ado/reference/rds-api/irdsservice-interface-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [Métodos RDS](../../../ado/reference/rds-api/rds-methods.md)


