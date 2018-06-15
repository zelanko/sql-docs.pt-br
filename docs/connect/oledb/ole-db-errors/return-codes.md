---
title: Códigos de retorno | Microsoft Docs
description: Códigos de retorno
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: b298d1900fcb61dd7b2e74586b7433eafd9dcf83
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35304635"
---
# <a name="return-codes"></a>Códigos de retorno
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  No nível mais básico, uma função de membro tem êxito ou falha. Em um nível um pouco mais preciso, uma função pode ser bem-sucedida, mas talvez seu êxito não seja o desejado pelo desenvolvedor do aplicativo.  
  
 Para obter mais informações sobre códigos de retorno de OLE DB, consulte [códigos de retorno (OLE DB)](http://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Quando um Driver OLE DB para a função de membro do SQL Server Retorna S_OK, a função foi bem-sucedida.  
  
 Quando um Driver OLE DB para a função de membro do SQL Server não retorna S_OK, as macros de descompactação de HRESULT de OLE/COM falha e IS_ERROR podem determinar o êxito ou falha de uma função geral.  
  
 Se FAILED ou IS_ERROR retornar TRUE, o Driver OLE DB para o consumidor do SQL Server terá certeza de que houve falha na execução da função de membro. Quando FAILED ou IS_ERROR retornar FALSE e o HRESULT não é igual a S_OK, o Driver OLE DB para SQL Server consumidor é garantido a função teve êxito em algum sentido. O consumidor pode recuperar informações detalhadas sobre este retorno de "êxito com informações" do Driver OLE DB para interfaces de erro do SQL Server. Além disso, no caso em que uma função falhar claramente (a macro FAILED retornar TRUE), as informações de erro estendidas estão disponíveis no Driver OLE DB para interfaces de erro do SQL Server.  
  
 OLE DB Driver para consumidores do SQL Server normalmente encontrar o retorno HRESULT DB_S_ERRORSOCCURRED "êxito com informações". Normalmente, funções de membro que retornam DB_S_ERRORSOCCURRED definem um ou mais parâmetros que fornecem valores de status ao consumidor. Nenhuma informação de erro pode estar disponível para o consumidor além daquela retornada em parâmetros de valor de status, para que os consumidores devem implementar a lógica do aplicativo para recuperar valores de status quando elas estão disponíveis.  
  
 O Driver OLE DB para funções de membro do SQL Server não retornam o código de êxito S_FALSE. Todas as OLE DB Driver para funções de membro do SQL Server sempre retornam S_OK para indicar êxito.  
  
## <a name="see-also"></a>Consulte também  
 [Erros](../../oledb/ole-db-errors/errors.md)  
  
  
