---
title: Propriedades (OLE DB) da fonte de dados | Microsoft Docs
description: Propriedades de fonte de dados (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: ef755447b9bb515fa6d05e1628ce7504e79f804a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-properties-ole-db"></a>Propriedades da fonte de dados (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O Driver OLE DB para SQL Server implementa propriedades da fonte de dados da seguinte maneira.  
  
|ID da propriedade|Description|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|Leitura/gravação: leitura/gravação Padrão: nenhum<br /><br /> Descrição: O valor de DBPROP_CURRENTCATALOG informa o banco de dados atual para um Driver OLE DB para a sessão do SQL Server. Definir o valor da propriedade tem o mesmo efeito que definir o banco de dados atual usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)] USE *banco de dados* instrução.<br /><br /> Começando com [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], se você chamar [sp_defaultdb](../../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md) e especifique o nome do banco de dados em minúsculas, mesmo se o banco de dados foi criado originalmente com um nome com maiusculas, DBPROP_CURRENTCATALOG retornará o nome em minúsculas. Nas versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], DBPROP_CURRENTCATALOG retornará as maiúsculas e minúsculas esperadas.|  
|DBPROP_MULTIPLECONNECTIONS|Leitura/gravação: leitura/gravação Padrão: VARIANT_FALSE<br /><br /> Descrição: se a conexão estiver executando um comando que não gera um conjunto de linhas ou que gera um conjunto de linhas que não é um cursor de servidor e você executar um outro comando, será criada uma nova conexão para executar o novo comando, se DBPROP_MULTIPLECONNECTIONS for VARIANT_TRUE.<br /><br /> O Driver OLE DB para SQL Server não criará outra conexão se DBPROP_MULTIPLECONNECTION for VARIANT_FALSE ou se uma transação está ativa na conexão. O Driver OLE DB para SQL Server retornará DB_E_OBJECTOPEN se DBPROP_MULTIPLECONNECTIONS for VARIANT_FALSE e retornará E_FAIL se houver uma transação ativa. As transações e o bloqueio são gerenciados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por conexão. Se uma segunda conexão for gerada, os comandos nas conexões separadas não compartilharão bloqueios. Para assegurar um comando não bloqueie o outro, mantenha os bloqueios em linhas solicitadas pelo outro comando. Isto também se aplica à criação de várias sessões.<br /><br /> Cada sessão tem uma conexão separada.|  
  
 No conjunto de propriedades específico do provedor DBPROPSET_SQLSERVERDATASOURCE, o Driver OLE DB para SQL Server define as seguintes propriedades de fonte de dados adicionais.  
  
|ID da propriedade|Description|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|Leitura/gravação: leitura/gravação Padrão: VARIANT_FALSE<br /><br /> Descrição: para habilitar a cópia em massa da memória, a propriedade SSPROP_ENABLEFASTLOAD deve ser definida como VARIANT_TRUE. Com essa propriedade definida na fonte de dados, a sessão recém-criada permite o acesso do consumidor para o [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md) interface.<br /><br /> Se a propriedade é definida como VARIANT_TRUE, **IRowsetFastLoad** interface está disponível por meio de **IOpenRowset:: OPENROWSET** solicitando o **IID_IRowsetFastLoad** interface ou definindo **SSPROP_IRowsetFastLoad** como VARIANT_TRUE.|  
|SSPROP_ENABLEBULKCOPY|Leitura/gravação: leitura/gravação Padrão: VARIANT_FALSE<br /><br /> Descrição: para habilitar a cópia em massa de arquivos, a propriedade SSPROP_ENABLEBULKCOPY deve ser definida como VARIANT_TRUE. Com essa propriedade definida na fonte de dados, o acesso do consumidor à interface IBCPSession está disponível no nível de Sessions.<br /><br /> SSPROP_IRowsetFastLoad também deve ser definido como VARIANT_TRUE.|  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de fonte de dados & #40; OLE DB & #41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
