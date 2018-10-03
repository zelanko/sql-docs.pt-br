---
title: Botões de navegação do catálogo de endereços | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS scenarios [ADO], navigation buttons
- address book application scenario [ADO], navigation buttons
ms.assetid: f0dd84c6-5c33-4ab9-82b4-4c42dfdd2277
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be8020f5a9ce826fbe4f92864d8d580bbcb6ae5a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696935"
---
# <a name="address-book-navigation-buttons"></a>Botões de navegação do catálogo de endereços
O aplicativo de catálogo de endereços exibe os botões de navegação na parte inferior da página da Web. Você pode usar os botões de navegação para navegar por meio dos dados na exibição de grade HTML selecionando a primeira ou última linha de dados ou linhas adjacentes à seleção atual.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="navigation-sub-procedures"></a>Navegação subprocedimentos  
 O aplicativo de catálogo de endereços contém vários procedimentos que permitem que os usuários cliquem a **primeira**, **próxima**, **anterior**, e **último** botões para mover os dados.  
  
 Por exemplo, clicar na **primeiro** botão ativa o procedimento de VBScript First_OnClick Sub. O procedimento executa um [MoveFirst](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) método, que torna a primeira linha de dados da seleção atual. Clicar na **última** botão ativa o procedimento de sub-rotina Last_OnClick, que invoca a [MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) método, tornando a última linha de dados da seleção atual. Os botões de navegação restantes funcionam de maneira semelhante.  
  
```  
' Move to the first record in the bound Recordset.  
Sub First_OnClick  
   DC1.Recordset.MoveFirst  
End Sub  
  
' Move to the next record from the current position   
' in the bound Recordset.  
Sub Next_OnClick  
   If Not DC1.Recordset.EOF Then    ' Cannot move beyond bottom record.  
      DC1.Recordset.MoveNext  
      Exit Sub  
   End If     
End Sub  
  
' Move to the previous record from the current position in the bound   
' Recordset.  
Sub Prev_OnClick  
   If Not DC1.Recordset.BOF Then    ' Cannot move beyond top record.  
      DC1.Recordset.MovePrevious  
      Exit Sub  
   End If  
End Sub  
  
' Move to the last record in the bound Recordset.  
Sub Last_OnClick  
   DC1.Recordset.MoveLast  
End Sub  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Métodos MoveFirst, MoveLast, MoveNext e MovePrevious (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)



