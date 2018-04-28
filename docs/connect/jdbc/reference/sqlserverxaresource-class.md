---
title: Classe SQLServerXAResource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: df957b79-536f-4db7-b6ac-3d59343559fc
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 64d2ae6fe7e4e57774dc75c34fc61ab680e99434
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlserverxaresource-class"></a>Classe SQLServerXAResource
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa um XAResource XA para o gerenciamento de transações distribuídas.  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** java.lang.Object  
  
 **Implementa:** javax  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public class SQLServerXAResource  
```  
  
## <a name="remarks"></a>Remarks  
 Transações XA são implementadas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] usando [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Gerenciador de transações distribuídas (DTC). A classe SQLServerXAResource faz chamadas para um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] estendido dll denominada sqljdbc_xa.dll, que interage com o DTC. As chamadas XA que são recebidas pelo SQLServerXAResource (XA_START, XA_END, XA_PREPARE e assim por diante) são mapeadas para as chamadas correspondentes às funções do DTC.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Referência da API do Driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
