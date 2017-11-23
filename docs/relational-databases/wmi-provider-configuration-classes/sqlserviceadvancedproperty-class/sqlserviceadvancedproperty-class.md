---
title: Classe SqlServiceAdvancedProperty | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: SqlServiceAdvancedProperty Class
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: SqlServiceAdvancedProperty class
ms.assetid: a5d06bde-6058-464c-a4aa-444d83f2331f
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cc15b15084f74c6749c1c3a33b34beadcb82d0a1
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sqlserviceadvancedproperty-class"></a>Classe SqlServiceAdvancedProperty
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]O [classe SqlServiceAdvancedProperty](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) representa uma propriedade avançada do serviço que é referenciado pelo [SqlService classe](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) objeto.  
  
 O [propriedade AdvancedProperties (classe SqlService)](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/advancedproperties-property-sqlservice-class.md) faz referência a uma matriz de [SqlServiceAdvancedProperty classe](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) objetos.  
  
 O [Iniciando e parando serviços](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx) classe representa propriedades que são exclusivas para o serviço. Essas propriedades não estão na lista de propriedades associada com o [SqlService classe](http://technet.microsoft.com/library/ms186497.aspx) classe. O [SqlServiceAdvancedProperty classe](http://technet.microsoft.com/library/ms182447.aspx) classe permite a representação de propriedades de cadeia de caracteres, numérico ou booleano. Você pode usar essa classe para exibir as propriedades exclusivas do serviço especificado.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando, parando e pausas serviços](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
