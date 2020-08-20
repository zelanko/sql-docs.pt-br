---
description: bcp_collen
title: bcp_collen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_collen
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_collen function
ms.assetid: faaf1f7a-81f2-4852-a178-56602c33673a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 33c0505109bebaba31e98c463cbb92b339af7e21
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499232"
---
# <a name="bcp_collen"></a>bcp_collen
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Define o comprimento de dados na variável de programa para a cópia em massa atual no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_collen (  
        HDBC hdbc,  
        DBINT cbData,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *cbData*  
 É o comprimento dos dados na variável de programa, não incluindo o comprimento dos indicadores ou terminadores de comprimento. A definição de *cbData* como SQL_NULL_DATA indica que todas as linhas copiadas no servidor contêm um valor NULL na coluna. Defini-lo como SQL_VARLEN_DATA indica que um terminador da cadeia de caracteres ou outro método é usado para determinar o comprimento dos dados copiados. Se um indicador de comprimento e um terminador existirem, o sistema usará o que resultar em menos cópia de dados.  
  
 *idxServerCol*  
 É a posição ordinal da coluna na tabela na qual os dados são copiados. A primeira coluna é 1. A posição ordinal de uma coluna é relatada por [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md).  
  
## <a name="returns"></a>Retornos  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
 A função **bcp_collen** permite que você altere o comprimento de dados na variável do programa para uma coluna específica quando copiar dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md).  
  
 Inicialmente, o comprimento de dados é determinado quando [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) é chamado. Se o comprimento de dados for alterado entre as chamadas para **bcp_sendrow** e nenhum prefixo de comprimento ou terminador for usado, você poderá chamar **bcp_collen** para redefinir o comprimento. A próxima chamada para **bcp_sendrow** usará o comprimento definido pela chamada para **bcp_collen**.  
  
 Você deve chamar **bcp_collen** uma vez para cada coluna na tabela cujo comprimento de dados deseje modificar.  
  
## <a name="see-also"></a>Consulte Também  
 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
