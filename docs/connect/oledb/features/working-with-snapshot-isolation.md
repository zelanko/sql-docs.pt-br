---
title: Trabalhando com isolamento de instantâneo | Microsoft Docs
description: Trabalhando com isolamento de instantâneo no Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], snapshot isolation
- MSOLEDBSQL, snapshot isolation
- isolation levels [SQL Server], snapshot
- DBPROPSET_SESSION property set
- DBDROPSET_DATASOURCEINFO property set
- snapshot isolation [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, snapshot isolation
- SQLGetInfo function
- concurrency [OLE DB Driver for SQL Server]
- SQLSetConnectAttr function
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c6fcec9fce11c4f03d92a28a0ae55ccb7e8f4d5c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="working-with-snapshot-isolation"></a>Trabalhando com isolamento de instantâneo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduziu um novo nível de isolamento de "instantâneo" cujo objeto é aumentar a simultaneidade para aplicativos OLTP (online transaction processing). Nas versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a simultaneidade baseava-se apenas no bloqueio, o que pode causar problemas de bloqueio e de deadlock em alguns aplicativos. O isolamento de instantâneo depende de aprimoramentos no controle de versão de linha e seu objetivo é melhorar o desempenho evitando cenários de bloqueio de leitor/gravador.  
  
 As transações que iniciam com o isolamento de instantâneo leem um instantâneo de banco de dados a partir da hora em que a transação inicia. Conjunto de chaves, cursores de servidor dinâmico e estático, aberto em um contexto de transação de instantâneo se comportam como muito parecido com Cursores estáticos abertos em transações serializáveis. No entanto, quando os cursores são abertos com os bloqueios de nível de isolamento de instantâneo não são aplicados. Esse fato pode reduzir o bloqueio no servidor.  
  
## <a name="ole-db-driver-for-sql-server"></a>Driver do OLE DB para SQL Server  
 O Driver OLE DB para SQL Server tem aprimoramentos que aproveitam o isolamento de instantâneo introduzido no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Esses aprimoramentos incluem alterações aos conjuntos de propriedades DBPROPSET_DATASOURCEINFO e DBPROPSET_SESSION.  
  
### <a name="dbpropsetdatasourceinfo"></a>DBPROPSET_DATASOURCEINFO  
 O conjunto de propriedades DBPROPSET_DATASOURCEINFO tem sido alterado para indicar que o nível de isolamento de instantâneo é suportado pela adição do valor DBPROPVAL_TI_SNAPSHOT usado na propriedade DBPROP_SUPPORTEDTXNISOLEVELS. Esse novo valor indica que haverá suporte para o nível de isolamento do instantâneo se o controle de versão tiver sido ou não habilitado no banco de dados. A tabela a seguir lista os valores DBPROP_SUPPORTEDTXNISOLEVELS:  
  
|ID da propriedade|Description|  
|-----------------|-----------------|  
|DBPROP_SUPPORTEDTXNISOLEVELS|Tipo: VT_I4<br /><br /> R/W: somente leitura<br /><br /> Descrição: Um bitmask que especifica os níveis de isolamento da transação com suporte. Uma combinação de zeros ou mais do seguinte:<br /><br /> DBPROPVAL_TI_CHAOS<br /><br /> DBPROPVAL_TI_READUNCOMMITTED<br /><br /> DBPROPVAL_TI_BROWSE<br /><br /> DBPROPVAL_TI_CURSORSTABILITY<br /><br /> DBPROPVAL_TI_READCOMMITTED<br /><br /> DBPROPVAL_TI_REPEATABLEREAD<br /><br /> DBPROPVAL_TI_SERIALIZABLE<br /><br /> DBPROPVAL_TI_ISOLATED<br /><br /> DBPROPVAL_TI_SNAPSHOT|  
  
### <a name="dbpropsetsession"></a>DBPROPSET_SESSION  
 O conjunto de propriedades DBPROPSET_SESSION tem sido alterado para indicar que o nível de isolamento de instantâneo é suportado pela adição do valor DBPROPVAL_TI_SNAPSHOT usado na propriedade DBPROP_SESS_AUTOCOMMITISOLEVELS. Esse novo valor indica que haverá suporte para o nível de isolamento do instantâneo se o controle de versão tiver sido ou não habilitado no banco de dados. A tabela a seguir lista os valores DBPROP_SESS_AUTOCOMMITISOLEVELS:
  
|ID da propriedade|Description|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|Tipo: VT_I4<br /><br /> R/W: somente leitura<br /><br /> Descrição: Especifica um bitmask que indica o nível de isolamento da transação enquanto estiver no modo de confirmação automática. Os valores que podem ser definidos nesse bitmask são iguais aos valores que podem ser definidos para DBPROP_SUPPORTEDTXNISOLEVELS.|  
  
> [!NOTE]  
>  Os erros DB_S_ERRORSOCCURRED ou DB_E_ERRORSOCCURRED ocorrerão se DBPROPVAL_TI_SNAPSHOT for definido durante o uso de versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Para obter informações sobre como suporte ao isolamento de instantâneo em transações, consulte [dando suporte a transações locais](../../oledb/ole-db-transactions/supporting-local-transactions.md).  

  
## <a name="see-also"></a>Consulte também  
 [Driver do OLE DB para recursos do SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [Comportamentos e propriedades de conjunto de linhas](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
  
