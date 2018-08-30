---
title: Classe SQLServerXAResource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: df957b79-536f-4db7-b6ac-3d59343559fc
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e7a40dc7a3f55a9c331f15783a4349e3ffbed269
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784147"
---
# <a name="sqlserverxaresource-class"></a>Classe SQLServerXAResource
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa um XAResource para o gerenciamento de transações distribuídas XA.  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** java.lang.Object  
  
 Implementa:** javax.transaction.xa.XAResource  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public class SQLServerXAResource  
```  
  
## <a name="remarks"></a>Remarks  
 As transações XA são implementadas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando o [!INCLUDE[msCoName](../../../includes/msconame_md.md)] DTC (Gerenciador de Transações Distribuídas). A classe [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]faz chamadas a uma dll estendida do  denominada sqljdbc_xa.dll, que faz interface com o DTC. As chamadas XA que são recebidas pela  (XA_START, XA_END, XA_PREPARE e assim por diante) são mapeadas para as chamadas correspondentes às funções do DTC.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Referência de API do JDBC Driver](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
