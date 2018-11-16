---
title: Códigos de retorno | Microsoft Docs
description: Códigos de retorno
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB error handling, return codes
- OLE DB Driver for SQL Server, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 0f09f9e2f9ad166edb764aa33a8b20623e11cf08
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600666"
---
# <a name="return-codes"></a>Códigos de retorno
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  No nível mais básico, uma função de membro tem êxito ou falha. Em um nível um pouco mais preciso, uma função pode ser bem-sucedida, mas talvez seu êxito não seja o desejado pelo desenvolvedor do aplicativo.  
  
 Para obter mais informações sobre códigos de retorno do OLE DB, confira [Códigos de retorno (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Quando um Driver OLE DB para a função de membro do SQL Server Retorna S_OK, a função foi bem-sucedida.  
  
 Quando uma função de membro do OLE DB Driver for SQL Server não retorna S_OK, as macros FAILED e IS_ERROR de descompactação de HRESULT de OLE/COM podem determinar o êxito ou a falha geral de uma função.  
  
 Se FAILED ou IS_ERROR retornar TRUE, o consumidor do OLE DB Driver for SQL Server terá certeza de que a execução da função de membro falhou. Quando FAILED ou IS_ERROR retornar FALSE e o HRESULT não é igual a S_OK, o Driver do OLE DB para SQL Server consumidor é garantido a função teve êxito em algum sentido. O consumidor pode recuperar informações detalhadas sobre este retorno de "êxito com informações" nas interfaces de erro do OLE DB Driver for SQL Server. Além disso, se uma função falhar claramente (a macro FAILED retorna TRUE), as informações de erro estendidas ficarão disponíveis nas interfaces de erro do OLE DB Driver for SQL Server.  
  
 Driver do OLE DB para consumidores do SQL Server normalmente encontram o retorno HRESULT DB_S_ERRORSOCCURRED "êxito com informações". Normalmente, funções de membro que retornam DB_S_ERRORSOCCURRED definem um ou mais parâmetros que fornecem valores de status ao consumidor. Talvez nenhuma informação de erro esteja disponível para o consumidor além daquela retornada em parâmetros de valor de status; assim, os consumidores deverão implementar a lógica de aplicativo para recuperar valores de status quando eles estiverem disponíveis.  
  
 O Driver do OLE DB para funções de membro do SQL Server não retornam o código de êxito S_FALSE. Todos os Driver do OLE DB para funções de membro do SQL Server sempre retornam S_OK para indicar êxito.  
  
## <a name="see-also"></a>Consulte Também  
 [Erros](../../oledb/ole-db-errors/errors.md)  
  
  
