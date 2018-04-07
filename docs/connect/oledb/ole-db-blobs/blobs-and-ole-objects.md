---
title: BLOBs e objetos OLE | Microsoft Docs
description: BLOBs e objetos OLE
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-blobs
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- OLE DB Driver for SQL Server, BLOBs
- large data, OLE objects
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6bc3707dca715ec5b6bee83d181c4792aea6c949
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="blobs-and-ole-objects"></a>BLOBs e objetos OLE
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O Driver OLE DB para SQL Server expõe o **ISequentialStream** interface para dar suporte ao acesso do consumidor para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **ntext**, **texto**, **imagem** , **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, e tipos de dados de xml binários como BLOBs (objetos grandes). O **leitura** método **ISequentialStream** permite que o consumidor recupere muitos dados em partes gerenciáveis.  
  
 Para obter um exemplo que demonstra esse recurso, consulte [do conjunto de dados grande & #40; OLE DB & #41;](../../oledb/ole-db-how-to/set-large-data-ole-db.md).  
  
 O Driver OLE DB para SQL Server pode usar um consumidor implementado **IStorage** interface quando o consumidor fornece o ponteiro de interface em um acessador associado para modificação de dados.  
  
 Para tipos de dados de valor grande, o Driver OLE DB para SQL Server procura suposições de tamanho do tipo em **IRowset** e interfaces DDL. Colunas que tenham **varchar**, **nvarchar**, e **varbinary** tipos de dados e tamanho máximo definido como ilimitado serão representadas como ISLONG por meio de conjuntos de linhas de esquema e pelo interfaces que retornam tipos de dados de coluna.  
  
 O Driver OLE DB para SQL Server expõe o **varchar (max)**, **varbinary (max)** e **nvarchar (max)** tipos como DBTYPE_STR, DBTYPE_BYTES e DBTYPE_WSTR, respectivamente.  
  
 Para trabalhar com esses tipos, um aplicativo tem as seguintes opções:  
  
-   Associar como o tipo (DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR). Se o buffer não é grande o suficiente ocorrerá truncamento, exatamente como para esses tipos em versões anteriores (embora valores maiores agora estão disponíveis).  
  
-   Associar como o tipo e também especificar DBTYPE_BYREF.  
  
-   Associar como DBTYPE_IUNKNOWN e usar streaming.  
  
 Se associado a DBTYPE_IUNKNOWN, é usada a funcionalidade de fluxo ISequentialStream. O Driver OLE DB para SQL Server dá suporte à associação de parâmetros de saída como DBTYPE_IUNKNOWN para tipos de dados de valor grande. Isso é para dar suporte a cenários onde um procedimento armazenado retorna esses tipos de dados como valores de retorno, serão retornados como DBTYPE_IUNKNOWN para o cliente.  
  
## <a name="storage-object-limitations"></a>Limitações de objetos de armazenamento  
  
-   O Driver OLE DB para SQL Server pode dar suporte a apenas um objeto de armazenamento aberto único. As tentativas de abrir mais de um objeto de armazenamento (para obter uma referência em mais de um **ISequentialStream** ponteiro de interface) retornam DBSTATUS_E_CANTCREATE.  
  
-   No OLE DB Driver para SQL Server, o valor padrão da propriedade somente leitura DBPROP_BLOCKINGSTORAGEOBJECTS é VARIANT_TRUE. Portanto, se um objeto de armazenamento está ativo, alguns métodos (diferentes métodos em objetos de armazenamento) falharão com E_UNEXPECTED.  
  
-   O comprimento dos dados apresentados por um objeto de armazenamento implementado pelo consumidor deve ser feito conhecido para o Driver OLE DB para SQL Server quando o acessador de linha que faz referência ao objeto de armazenamento é criado. O consumidor deve associar um indicador de comprimento na estrutura DBBINDING usada para a criação do acessador.  
  
-   Se uma linha contiver mais de um valor único de dados grande e DBPROP_ACCESSORDER não for DBPROPVAL_AO_RANDOM, o consumidor deve usar um Driver OLE DB para SQL Server com suporte de cursor linhas para recuperar dados de linha ou processar todos os valores de dados grandes antes de recuperar outros valores de linha. Se DBPROP_ACCESSORDER for DBPROPVAL_AO_RANDOM, o Driver OLE DB para SQL Server armazena em cache todos os tipos de dados xml como objetos binários grandes (BLOBs) para que ele possa ser acessado em qualquer ordem.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Obtendo dados grandes](../../oledb/ole-db-blobs/getting-large-data.md)  
  
-   [Definir dados grandes](../../oledb/ole-db-blobs/setting-large-data.md)  
  
-   [Suporte de streaming para parâmetros de saída BLOB](../../oledb/ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>Consulte também  
 [Driver do OLE DB para SQL Server &#40;OLE DB&#41;](../../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)        
 [Usando tipos de valor grande](../../oledb/features/using-large-value-types.md)  
  
  
