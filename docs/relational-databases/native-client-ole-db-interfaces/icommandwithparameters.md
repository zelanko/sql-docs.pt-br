---
description: ICommandWithParameters (provedor de OLE DB de cliente nativo)
title: ICommandWithParameters (provedor de OLE DB de cliente nativo) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 66644c70-def7-46d8-8c47-b883292a0288
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1f23eeff801717661305dafac67939990545e43a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473437"
---
# <a name="icommandwithparameters-native-client-ole-db-provider"></a>ICommandWithParameters (provedor de OLE DB de cliente nativo)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Aprimoramentos no mecanismo de banco de dados desde o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permitem que ICommandWithParameters::GetParameterInfo obtenha descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados por CommandWithParameters::GetParameterInfo em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Descoberta de metadados](../../relational-databases/native-client/features/metadata-discovery.md).  
  
 Além disso, do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] em diante, ao chamar ICommandWithParameters::SetParameterInfo, o valor passado para o parâmetro *pwszName* precisa ser um identificador válido. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces do &#40;OLE DB&#41;](./sql-server-native-client-ole-db-interfaces.md)  
  
