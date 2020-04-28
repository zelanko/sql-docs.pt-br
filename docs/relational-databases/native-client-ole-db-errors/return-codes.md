---
title: Códigos de retorno | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB error handling, return codes
- SQL Server Native Client OLE DB provider, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
ms.assetid: 7f7457e9-fce4-400c-82e5-ee02e9e811c6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 09056c9d4964ad10b2b25f63ef5991a1a7742cab
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301008"
---
# <a name="return-codes"></a>Códigos de retorno
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  No nível mais básico, uma função de membro tem êxito ou falha. Em um nível um pouco mais preciso, uma função pode ser bem-sucedida, mas talvez seu êxito não seja o desejado pelo desenvolvedor do aplicativo.  
  
 Para obter mais informações sobre códigos de retorno do OLE DB, confira [Códigos de retorno (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Quando uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de membro de provedor de OLE DB de cliente nativo retorna S_OK, a função foi bem-sucedida.  
  
 Quando uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de membro de provedor de OLE DB de cliente nativo não retorna S_OK, o OLE/com HRESULT-desempacotamento falhou e IS_ERROR macros podem determinar o êxito geral ou a falha de uma função.  
  
 Se a falha ou IS_ERROR retornar TRUE, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o consumidor do provedor de OLE DB de cliente nativo terá a garantia de que a execução da função de membro falhou. Quando com falha ou IS_ERROR retornar FALSE e o HRESULT não for igual a S_OK [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o cliente do provedor de OLE DB do Native Client terá certeza de que a função teve êxito em algum sentido. O consumidor pode recuperar informações detalhadas sobre esse retorno de "êxito com informações" das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces de erro do provedor de OLE DB de cliente nativo. Além disso, no caso em que uma função falha claramente (a macro com falha retorna TRUE), as informações de erro estendidas estão disponíveis nas interfaces de erro do provedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB de cliente nativo.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Os consumidores do provedor de OLE DB de cliente nativo geralmente encontram o DB_S_ERRORSOCCURRED "sucesso com informações" de retorno de HRESULT. Normalmente, funções de membro que retornam DB_S_ERRORSOCCURRED definem um ou mais parâmetros que fornecem valores de status ao consumidor. Talvez nenhuma informação de erro esteja disponível para o consumidor além daquela retornada em parâmetros de valor de status; assim, os consumidores devem implementar a lógica de aplicativo para recuperar valores de status quando eles estiverem disponíveis.  
  
 As [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funções de membro do provedor de OLE DB de cliente nativo não retornam o código de êxito S_FALSE. Todas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as funções de membro do provedor de OLE DB de cliente nativo sempre retornam S_OK para indicar êxito.  
  
## <a name="see-also"></a>Consulte Também  
 [Errors](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
