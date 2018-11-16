---
title: MoveFirst, MoveLast, MoveNext e MovePrevious métodos (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3afc55ca26a8462eb5662287288ee885f9104a8c
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606668"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-rds"></a>Métodos MoveFirst, MoveLast, MoveNext e MovePrevious (RDS)
Move para a primeira, última, registro anterior ou seguinte em um especificado [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.Recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
## <a name="remarks"></a>Comentários  
 Você pode usar o **mova** métodos com o **RDS. DataControl** objeto para percorrer os registros de dados nos controles ligados a dados em uma página da Web. Por exemplo, suponha que você exiba uma **conjunto de registros** em uma grade fazendo a ligação com um **RDS. DataControl** objeto. Em seguida, você pode incluir botões First, Last, próximo e anterior que os usuários podem clicar para mover para a primeira, última, em seguida, ou o registro anterior na exibidos **conjunto de registros**. Você pode fazer isso chamando o **MoveFirst**, **MoveLast**, **MoveNext**, e **MovePrevious** métodos do **RDS. DataControl** do objeto nos procedimentos onClick para os botões First, Last, próximo e anterior, respectivamente. O [exemplo de catálogo de endereços](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md) mostra como fazer isso.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método Move (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext e MovePrevious métodos (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)


