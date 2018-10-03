---
title: BLOBs e objetos OLE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- SQL Server Native Client OLE DB provider, BLOBs
- large data, OLE objects
ms.assetid: 767fa2f6-9cd2-436f-add5-e760bed29a58
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e459682da63bac8359fa8310233c234e456f4e5b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48180316"
---
# <a name="blobs-and-ole-objects"></a>BLOBs e objetos OLE
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client expõe a **ISequentialStream** interface para dar suporte ao acesso do consumidor a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ntext**, **texto**, **imagem**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, e os tipos de dados xml como binários BLOBs (objetos grandes ). O método **Read** em **ISequentialStream** permite que o consumidor recupere muitos dados em partes gerenciáveis.  
  
 Para obter um exemplo que demonstra este recurso, consulte [do conjunto de dados grandes &#40;OLE DB&#41;](../native-client-ole-db-how-to/set-large-data-ole-db.md).  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client pode usar um consumidor implementado **IStorage** interface quando o consumidor fornece o ponteiro de interface em um acessador associado para modificação de dados.  
  
 Para tipos de dados de valor grande, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client verifica as suposições de tamanho de tipo no **IRowset** e interfaces DDL. Colunas com **varchar**, **nvarchar**, e **varbinary** tipos de dados com tamanho máximo definido como ilimitado serão representados como ISLONG por meio de conjuntos de linhas de esquema e interfaces retornando tipos de dados de coluna.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client expõe a **varchar (max)**, **varbinary (max)** e **nvarchar (max)** tipos como DBTYPE_STR, DBTYPE_BYTES e DbType _ WSTR, respectivamente.  
  
 Para trabalhar com esses tipos de um aplicativo tem as seguintes opções:  
  
-   Associar como o tipo (DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR). Se o buffer não for suficientemente grande, ocorrerá truncamento, exatamente como para esses tipos em versões anteriores (embora agora haja valores maiores disponíveis).  
  
-   Associar como o tipo e também especificar DBTYPE_BYREF.  
  
-   Associar como DBTYPE_IUNKNOWN e usar streaming.  
  
 Se associado a DBTYPE_IUNKNOWN, é usada a funcionalidade de fluxo ISequentialStream. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client dá suporte a parâmetros de saída de associação como DBTYPE_IUNKNOWN para tipos de dados de valor grande facilitar cenários em que um procedimento armazenado retorna esses dados de tipos como valores de retorno que será exposto como DBTYPE_IUNKNOWN para o cliente.  
  
## <a name="storage-object-limitations"></a>Limitações de objetos de armazenamento  
  
-   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client pode dar suporte a apenas um objeto único armazenamento aberto. As tentativas de abrir mais de um objeto de armazenamento (para obter uma referência em mais de um ponteiro da interface **ISequentialStream**) retornam DBSTATUS_E_CANTCREATE.  
  
-   No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client, o valor padrão da propriedade somente leitura DBPROP_BLOCKINGSTORAGEOBJECTS é VARIANT_TRUE. Isso indica que se um objeto de armazenamento está ativo, alguns métodos (diferentes daqueles nos objetos de armazenamento) falharão com E_UNEXPECTED.  
  
-   O comprimento dos dados apresentados por um objeto implementado pelo cliente de armazenamento deve ser feito conhecido para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client quando o acessador de linha que faz referência ao objeto de armazenamento é criado. O consumidor deve associar um indicador de comprimento na estrutura DBBINDING usada para a criação do acessador.  
  
-   Se uma linha contiver mais de um valor de dados grande e DBPROP_ACCESSORDER não for DBPROPVAL_AO_RANDOM, o consumidor deverá usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB do Native Client com suporte de cursor linhas para recuperar dados de linha ou processar dados de todos os grandes valores antes de Recuperando valores de outras linhas. Se DBPROP_ACCESSORDER for DBPROPVAL_AO_RANDOM, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client armazena em cache todos os tipos de dados xml como objetos binários grandes (BLOBs) para que ele possa ser acessado em qualquer ordem.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Obtendo dados grandes](getting-large-data.md)  
  
-   [Configurando dados grandes](setting-large-data.md)  
  
-   [Suporte de streaming para parâmetros de saída BLOB](streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)   
 [Usando tipos de valor grande](../native-client/features/using-large-value-types.md)  
  
  
