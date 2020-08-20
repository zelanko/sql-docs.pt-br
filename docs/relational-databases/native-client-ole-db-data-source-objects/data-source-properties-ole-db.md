---
description: Propriedades da fonte de dados de SQL Server Native Client (OLE DB)
title: Propriedades da fonte de dados (provedor de OLE DB de cliente nativo) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 6e14fefc-4e0b-4847-a833-4cf0abe65d50
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e26ea91c7734a4cff58b2cf026ee17cadcdf2e9a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455992"
---
#  <a name="sql-server-native-client-data-source-properties-ole-db"></a>Propriedades da fonte de dados de SQL Server Native Client (OLE DB)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo implementa as propriedades da fonte de dados da seguinte maneira.  
  
|ID da propriedade|DESCRIÇÃO|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|Leitura/gravação: leitura/gravação Padrão: nenhum<br /><br /> Descrição: o valor de DBPROP_CURRENTCATALOG relata o banco de dados atual para uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sessão de provedor de OLE DB de cliente nativo. A definição do valor da propriedade tem o mesmo efeito de definir o banco de dados atual usando a instrução USE *database* do [!INCLUDE[tsql](../../includes/tsql-md.md)].<br /><br /> Do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] em diante, se você chamar [sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md) e especificar o nome do banco de dados em minúsculas, mesmo que o banco de dados tenha sido criado originalmente com um nome com maiúsculas e minúsculas, DBPROP_CURRENTCATALOG retornará o nome em minúsculas. Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], DBPROP_CURRENTCATALOG retornará as maiúsculas e minúsculas esperadas.|  
|DBPROP_MULTIPLECONNECTIONS|Leitura/gravação: leitura/gravação Padrão: VARIANT_FALSE<br /><br /> Descrição: se a conexão estiver executando um comando que não gera um conjunto de linhas ou que gera um conjunto de linhas que não é um cursor de servidor e você executar um outro comando, será criada uma nova conexão para executar o novo comando, se DBPROP_MULTIPLECONNECTIONS for VARIANT_TRUE.<br /><br /> O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo não criará outra conexão se DBPROP_MULTIPLECONNECTION estiver VARIANT_FALSE ou se uma transação estiver ativa na conexão. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo retorna DB_E_OBJECTOPEN se DBPROP_MULTIPLECONNECTIONS é VARIANT_FALSE e retorna E_FAIL se houver uma transação ativa. As transações e o bloqueio são gerenciados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por conexão. Se uma segunda conexão for gerada, os comandos nas conexões separadas não compartilharão bloqueios. Para assegurar um comando não bloqueie o outro, mantenha os bloqueios em linhas solicitadas pelo outro comando. Isto também se aplica à criação de várias sessões.<br /><br /> Cada sessão tem uma conexão separada.|  
  
 No conjunto de propriedades específico do provedor DBPROPSET_SQLSERVERDATASOURCE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo define as propriedades de fonte de dados adicionais a seguir.  
  
|ID da propriedade|DESCRIÇÃO|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|Leitura/gravação: leitura/gravação Padrão: VARIANT_FALSE<br /><br /> Descrição: para habilitar a cópia em massa da memória, a propriedade SSPROP_ENABLEFASTLOAD deve ser definida como VARIANT_TRUE. Com essa propriedade definida na fonte de dados, a sessão recém-criada permite que o consumidor acesse a interface [IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md).<br /><br /> Se a propriedade for definida como VARIANT_TRUE, a interface **IRowsetFastLoad** ficará disponível por meio de **IOpenRowset::OpenRowset**, solicitando a interface **IID_IRowsetFastLoad** ou definindo **SSPROP_IRowsetFastLoad** como VARIANT_TRUE.|  
|SSPROP_ENABLEBULKCOPY|Leitura/gravação: leitura/gravação Padrão: VARIANT_FALSE<br /><br /> Descrição: para habilitar a cópia em massa de arquivos, a propriedade SSPROP_ENABLEBULKCOPY deve ser definida como VARIANT_TRUE. Com essa propriedade definida na fonte de dados, o acesso do consumidor à interface IBCPSession está disponível no nível de Sessions.<br /><br /> SSPROP_IRowsetFastLoad também deve ser definido como VARIANT_TRUE.|  
  
## <a name="see-also"></a>Consulte Também  
 [Objetos de fonte de dados &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
