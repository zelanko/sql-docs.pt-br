---
title: Propriedades (OLE DB) da fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 6e14fefc-4e0b-4847-a833-4cf0abe65d50
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 094bcbe48fa6c4cf09120b1dcf835c08199f10d1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074120"
---
# <a name="data-source-properties-ole-db"></a>Propriedades da fonte de dados (OLE DB)
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client implementa propriedades da fonte de dados da seguinte maneira.  
  
|ID da propriedade|Description|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|Leitura/gravação: leitura/gravação Padrão: nenhum<br /><br /> Descrição: O valor de DBPROP_CURRENTCATALOG informa o banco de dados atual para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sessão do provedor OLE DB do Native Client. A definição do valor da propriedade tem o mesmo efeito de definir o banco de dados atual usando a instrução USE *database* do [!INCLUDE[tsql](../../includes/tsql-md.md)].<br /><br /> Do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] em diante, se você chamar [sp_defaultdb](/sql/relational-databases/system-stored-procedures/sp-defaultdb-transact-sql) e especificar o nome do banco de dados em minúsculas, mesmo que o banco de dados tenha sido criado originalmente com um nome com maiúsculas e minúsculas, DBPROP_CURRENTCATALOG retornará o nome em minúsculas. Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], DBPROP_CURRENTCATALOG retornará as maiúsculas e minúsculas esperadas.|  
|DBPROP_MULTIPLECONNECTIONS|Leitura/gravação: leitura/gravação Padrão: VARIANT_FALSE<br /><br /> Descrição: se a conexão estiver executando um comando que não gera um conjunto de linhas ou que gera um conjunto de linhas que não é um cursor de servidor e você executar um outro comando, será criada uma nova conexão para executar o novo comando, se DBPROP_MULTIPLECONNECTIONS for VARIANT_TRUE.<br /><br /> O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client não criará outra conexão se DBPROP_MULTIPLECONNECTION for VARIANT_FALSE ou se uma transação está ativa na conexão. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client retornará DB_E_OBJECTOPEN se DBPROP_MULTIPLECONNECTIONS for VARIANT_FALSE e retornará E_FAIL se houver uma transação ativa. As transações e o bloqueio são gerenciados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por conexão. Se uma segunda conexão for gerada, os comandos nas conexões separadas não compartilharão bloqueios. Para assegurar um comando não bloqueie o outro, mantenha os bloqueios em linhas solicitadas pelo outro comando. Isto também se aplica à criação de várias sessões.<br /><br /> Cada sessão tem uma conexão separada.|  
  
 Na propriedade específica do provedor definida DBPROPSET_SQLSERVERDATASOURCE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client define as seguintes propriedades de fonte de dados adicionais.  
  
|ID da propriedade|Description|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|Leitura/gravação: leitura/gravação Padrão: VARIANT_FALSE<br /><br /> Descrição: para habilitar a cópia em massa da memória, a propriedade SSPROP_ENABLEFASTLOAD deve ser definida como VARIANT_TRUE. Com essa propriedade definida na fonte de dados, a sessão recém-criada permite que o consumidor acesse a interface [IRowsetFastLoad](../native-client-ole-db-interfaces/irowsetfastload-ole-db.md).<br /><br /> Se a propriedade for definida como VARIANT_TRUE, a interface **IRowsetFastLoad** ficará disponível por meio de **IOpenRowset::OpenRowset**, solicitando a interface **IID_IRowsetFastLoad** ou definindo **SSPROP_IRowsetFastLoad** como VARIANT_TRUE.|  
|SSPROP_ENABLEBULKCOPY|Leitura/gravação: leitura/gravação Padrão: VARIANT_FALSE<br /><br /> Descrição: para habilitar a cópia em massa de arquivos, a propriedade SSPROP_ENABLEBULKCOPY deve ser definida como VARIANT_TRUE. Com essa propriedade definida na fonte de dados, o acesso do consumidor à interface IBCPSession está disponível no nível de Sessions.<br /><br /> SSPROP_IRowsetFastLoad também deve ser definido como VARIANT_TRUE.|  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de fonte de dados &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
