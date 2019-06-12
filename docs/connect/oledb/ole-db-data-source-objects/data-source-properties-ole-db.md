---
title: Propriedades (OLE DB) da fonte de dados | Microsoft Docs
description: Propriedades de fonte de dados (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: c97c85eaeafd7d811b3f513f7f9cccc30c873b71
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66768646"
---
# <a name="data-source-properties-ole-db"></a>Propriedades da fonte de dados (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver do OLE DB para SQL Server implementa propriedades da fonte de dados da seguinte maneira.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|Leitura/gravação: leitura/gravação Padrão: nenhum<br /><br /> Descrição: o valor de DBPROP_CURRENTCATALOG relata o banco de dados atual para uma sessão do OLE DB Driver for SQL Server. A definição do valor da propriedade tem o mesmo efeito de definir o banco de dados atual usando a instrução USE *database* do [!INCLUDE[tsql](../../../includes/tsql-md.md)].<br /><br /> Do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] em diante, se você chamar [sp_defaultdb](../../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md) e especificar o nome do banco de dados em minúsculas, mesmo que o banco de dados tenha sido criado originalmente com um nome com maiúsculas e minúsculas, DBPROP_CURRENTCATALOG retornará o nome em minúsculas. Nas versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], DBPROP_CURRENTCATALOG retornará as maiúsculas e minúsculas esperadas.|  
|DBPROP_MULTIPLECONNECTIONS|Leitura/gravação: leitura/gravação Padrão: VARIANT_FALSE<br /><br /> Descrição: se a conexão estiver executando um comando que não gera um conjunto de linhas ou que gera um conjunto de linhas que não é um cursor de servidor e você executar um outro comando, será criada uma nova conexão para executar o novo comando, se DBPROP_MULTIPLECONNECTIONS for VARIANT_TRUE.<br /><br /> O OLE DB Driver for SQL Server não criará outra conexão se DBPROP_MULTIPLECONNECTION for VARIANT_FALSE ou se houver uma transação ativa na conexão. O OLE DB Driver for SQL Server retorna DB_E_OBJECTOPEN se DBPROP_MULTIPLECONNECTIONS é VARIANT_FALSE e retorna E_FAIL se há uma transação ativa. As transações e o bloqueio são gerenciados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por conexão. Se uma segunda conexão for gerada, os comandos nas conexões separadas não compartilharão bloqueios. Para assegurar um comando não bloqueie o outro, mantenha os bloqueios em linhas solicitadas pelo outro comando. Isto também se aplica à criação de várias sessões.<br /><br /> Cada sessão tem uma conexão separada.|  
  
 No conjunto de propriedades específico do provedor DBPROPSET_SQLSERVERDATASOURCE, o OLE DB Driver for SQL Server define as propriedades de fonte de dados adicionais a seguir.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|Leitura/gravação: leitura/gravação Padrão: VARIANT_FALSE<br /><br /> Descrição: para habilitar a cópia em massa da memória, a propriedade SSPROP_ENABLEFASTLOAD deve ser definida como VARIANT_TRUE. Com essa propriedade definida na fonte de dados, a sessão recém-criada permite que o consumidor acesse a interface [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md).<br /><br /> Se a propriedade for definida como VARIANT_TRUE, a interface **IRowsetFastLoad** ficará disponível por meio de **IOpenRowset::OpenRowset**, solicitando a interface **IID_IRowsetFastLoad** ou definindo **SSPROP_IRowsetFastLoad** como VARIANT_TRUE.|  
|SSPROP_ENABLEBULKCOPY|Leitura/gravação: leitura/gravação Padrão: VARIANT_FALSE<br /><br /> Descrição: para habilitar a cópia em massa de arquivos, a propriedade SSPROP_ENABLEBULKCOPY deve ser definida como VARIANT_TRUE. Com essa propriedade definida na fonte de dados, o acesso do consumidor à interface IBCPSession está disponível no nível de Sessions.<br /><br /> SSPROP_IRowsetFastLoad também deve ser definido como VARIANT_TRUE.|  
  
## <a name="see-also"></a>Consulte Também  
 [Objetos de fonte de dados &#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
