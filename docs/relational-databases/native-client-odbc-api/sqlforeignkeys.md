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
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d59eb895b735771a94fa04745b492fc68eb2ea74
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63014500"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a atualizações e exclusões em cascata por meio do mecanismo de restrição de chave estrangeira. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará SQL_CASCADE para as colunas UPDATE_RULE e/ou DELETE_RULE se a opção CASCADE estiver especificada na cláusula ON UPDATE e/ou ON DELETE das restrições FOREIGN KEY. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará SQL_NO_ACTION para as colunas UPDATE_RULE e/ou DELETE_RULE se a opção NO ACTION estiver especificada na cláusula ON UPDATE e/ou ON DELETE das restrições FOREIGN KEY.  
  
 Quando valores inválidos estiverem presentes em qualquer **SQLForeignKeys** parâmetro, **SQLForeignKeys** retornará SQL_SUCCESS na execução. **SQLFetch** retorna SQL_NO_DATA quando são usados valores inválidos nesses parâmetros.  
  
 **SQLForeignKeys** pode ser executado em um cursor de servidor estático. Uma tentativa de executar **SQLForeignKeys** em um cursor atualizável (dinâmico ou conjunto de chaves) retornará SQL_SUCCESS_WITH_INFO, indicando que o tipo de cursor foi alterado.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client dá suporte a informações de relatórios para tabelas em servidores vinculados, aceitando um nome de duas partes para o *FKCatalogName* e *PKCatalogName* parâmetros: *Linked_server_name*.  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLForeignKeys](https://go.microsoft.com/fwlink/?LinkId=59344)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
