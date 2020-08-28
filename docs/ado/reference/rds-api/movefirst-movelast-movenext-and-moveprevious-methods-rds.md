---
description: Métodos MoveFirst, MoveLast, MoveNext e MovePrevious (RDS)
title: Métodos MoveFirst, MoveLast, MoveNext e MovePrevious (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- MoveLast method [RDS]
- MovePrevious method [RDS]
- MoveFirst method [RDS]
- MoveNext method [RDS]
ms.assetid: 45c80bb5-136f-4204-9df2-78740fa55574
author: rothja
ms.author: jroth
ms.openlocfilehash: 8feb41ff7ff1069d29beacc3b5dc0d323cdfd72b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88981907"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-rds"></a>Métodos MoveFirst, MoveLast, MoveNext e MovePrevious (RDS)
Move para o primeiro, o último, o próximo ou o registro anterior em um objeto [Recordset](../ado-api/recordset-object-ado.md) especificado.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.Recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. Objeto DataControl](./datacontrol-object-rds.md) .  
  
## <a name="remarks"></a>Comentários  
 Você pode usar os métodos **move** com o **RDS. Objeto DataControl** para navegar pelos registros de dados nos controles associados a dados em uma página da Web. Por exemplo, suponha que você exiba um **conjunto de registros** em uma grade ligando a um **RDS. Objeto DataControl** . Em seguida, você pode incluir os botões primeiro, último, avançar e anterior que os usuários podem clicar para mover para o primeiro, o último, o próximo ou o registro anterior no **conjunto de registros**exibido. Faça isso chamando os métodos **MoveFirst**, **MoveLast**, **MoveNext**e **MovePrevious** do **RDS. Objeto DataControl** nos procedimentos OnClick para os botões primeiros, último, próximo e anterior, respectivamente. O [exemplo de catálogo de endereços](../../guide/remote-data-service/address-book-navigation-buttons.md) mostra como fazer isso.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método Move (ADO)](../ado-api/move-method-ado.md)   
 [Métodos MoveFirst, MoveLast, MoveNext e MovePrevious (ADO)](../ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Método MoveRecord (ADO)](../ado-api/moverecord-method-ado.md)