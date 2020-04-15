---
title: Erros | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
ms.assetid: bd0612f4-96ef-4919-b0f9-b5447210fe93
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 396d70beabab15d715a99cfd9df074fd75091ca2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302296"
---
# <a name="errors"></a>Errors
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Os objetos OLE/COM informam erros através do código de retorno de HRESULT das funções de membro de objeto. Um HRESULT de OLE/COM é uma estrutura de bits compactados. A OLE fornece macros que eliminam a referência de membros de estrutura.  
  
 O OLE/COM especifica a interface **IErrorInfo**. A interface expõe métodos como **GetDescription**. Isso permite que clientes extraiam detalhes de erros dos servidores OLE/COM. O OLE DB estende **IErrorInfo** para dar suporte ao retorno de vários pacotes de informações de erros em uma execução de função de único membro.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode retornar vários erros. Um aplicativo pode recuperar erros do servidor um de cada vez chamando [IMultipleResults::GetResult](https://go.microsoft.com/fwlink/?LinkId=129630) combinado com ISQLErrorInfo e IErrorRecords.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Nativo Cliente OLE DB expõe o **IErrorInfo**aprimorado pelo registro OLE DB, o **ISQLErrorInfo**personalizado e as interfaces de objeto de erro [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) específicas do provedor.  
  
 Para obter informações sobre como rastrear erros, confira [Rastreamento do acesso a dados](https://go.microsoft.com/fwlink/?LinkId=125805). Para obter informações sobre aprimoramentos no rastreamento de erros adicionados em [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], confira [Acessar informações de diagnóstico nos logs de eventos estendidos](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Códigos de retorno](../../relational-databases/native-client-ole-db-errors/return-codes.md)  
  
-   [Informações em interfaces de erro](../../relational-databases/native-client-ole-db-errors/information-in-error-interfaces.md)  
  
-   [Detalhes de erros do SQL Server](../../relational-databases/native-client-ole-db-errors/sql-server-error-detail.md)  
  
-   [Recuperando informações de erro](../../relational-databases/native-client-ole-db-errors/retrieving-error-information.md)  
  
-   [Resultados da mensagem do SQL Server](../../relational-databases/native-client-ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
