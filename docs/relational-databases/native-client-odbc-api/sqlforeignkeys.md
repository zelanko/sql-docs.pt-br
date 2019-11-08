---
title: SQLForeignKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLForeignKeys function
ms.assetid: 6c01ce0d-30d7-4c86-8705-3ab254d8a845
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c8e3cee37a124c40c21e6d8ee8829dcf7f39e808
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73786827"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a atualizações e exclusões em cascata por meio do mecanismo de restrição de chave estrangeira. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará SQL_CASCADE para as colunas UPDATE_RULE e/ou DELETE_RULE se a opção CASCADE estiver especificada na cláusula ON UPDATE e/ou ON DELETE das restrições FOREIGN KEY. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará SQL_NO_ACTION para as colunas UPDATE_RULE e/ou DELETE_RULE se a opção NO ACTION estiver especificada na cláusula ON UPDATE e/ou ON DELETE das restrições FOREIGN KEY.  
  
 Quando valores inválidos estão presentes em qualquer parâmetro **SQLForeignKeys** , **SQLForeignKeys** retorna SQL_SUCCESS na execução. **SQLFetch** retorna SQL_NO_DATA quando são usados valores inválidos nesses parâmetros.  
  
 **SQLForeignKeys** pode ser executado em um cursor de servidor estático. Uma tentativa de executar **SQLForeignKeys** em um cursor atualizável (dinâmico ou de conjunto de chaves) retorna SQL_SUCCESS_WITH_INFO indicando que o tipo de cursor foi alterado.  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte a informações de relatório para tabelas em servidores vinculados, aceitando um nome de duas partes para os parâmetros *FKCatalogName* e *PKCatalogName* : *linked_server_name. catalog_name*.  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLForeignKeys](https://go.microsoft.com/fwlink/?LinkId=59344)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
