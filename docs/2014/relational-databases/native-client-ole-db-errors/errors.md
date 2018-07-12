---
title: Erros | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
ms.assetid: bd0612f4-96ef-4919-b0f9-b5447210fe93
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac616813b3437c57a8e071ea876874880874f039
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424665"
---
# <a name="errors"></a>Erros
  Os objetos OLE/COM informam erros através do código de retorno de HRESULT das funções de membro de objeto. Um HRESULT de OLE/COM é uma estrutura de bits compactados. A OLE fornece macros que eliminam a referência de membros de estrutura.  
  
 OLE/COM Especifica a **IErrorInfo** interface. A interface expõe métodos como **GetDescription**. Isso permite que clientes extraiam detalhes de erros dos servidores OLE/COM. OLE DB estende **IErrorInfo** para suportar o retorno de vários pacotes de informações de erro em uma execução de função de membro único.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode retornar vários erros. Um aplicativo pode recuperar erros do servidor um por vez chamando [imultipleresults:: GetResult](http://go.microsoft.com/fwlink/?LinkId=129630) combinado com ISQLErrorInfo e IErrorRecords.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client expõe o OLE DB aprimorada de registro **IErrorInfo**, personalizado `ISQLErrorInfo`e específicas do provedor [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) objeto error interfaces.  
  
 Para obter informações sobre rastreamento de erros, consulte [rastreamento do acesso a dados](http://go.microsoft.com/fwlink/?LinkId=125805). Para obter informações sobre os aprimoramentos para rastreamento de erro adicionado ao [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], consulte [acessando informações de diagnóstico no Log de eventos estendidos](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Códigos de retorno](return-codes.md)  
  
-   [Informações em interfaces de erro](information-in-error-interfaces.md)  
  
-   [Detalhes de erros do SQL Server](sql-server-error-detail.md)  
  
-   [Recuperando informações de erro](retrieving-error-information.md)  
  
-   [Resultados da mensagem do SQL Server](sql-server-message-results.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
