---
description: Classe SqlServerAlias
title: Classe SqlServerAlias
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- SqlServerAlias Class
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServerAlias class
ms.assetid: 475662b9-6985-45bf-b1e9-b0f26ef50443
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d3acca52f0139cf0f7ef6085470a5d9e2b839494
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550876"
---
# <a name="sqlserveralias-class"></a>Classe SqlServerAlias
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  A classe [da classe SqlServerAlias](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) representa um alias de conexão de servidor.  
  
 Um alias de conexão de servidor é necessário quando as seguintes situações ocorrerem:  
  
-   O cliente está se conectando a uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em um transporte de rede que não é o transporte de rede padrão.  
  
-   A instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para o qual o cliente é conectado escuta em um pipe nomeado alternativo.  
  
 **Observação:** A [classe SqlServerAlias](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) herda o método **Put** da classe Provider. Porém, ela não retorna nenhum resultado como indicado pelo método **Provider::Put** . Para obter mais informações, consulte a documentação do WMI.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
