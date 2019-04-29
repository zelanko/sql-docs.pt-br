---
title: Parâmetros com valor de tabela (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
ms.assetid: 4298b73d-615b-4d28-9843-03b4d5fc489e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9c58b1837eb017a3cc51652ff404b37690b3849
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046420"
---
# <a name="table-valued-parameters-ole-db"></a>Parâmetros com valor de tabela (OLE DB)
  Esta seção descreve o suporte a parâmetros com valor de tabela no provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Para obter informações gerais adicionais, consulte [parâmetros com valor de tabela &#40;SQL Server Native Client&#41;](../native-client/features/table-valued-parameters-sql-server-native-client.md). Para obter um exemplo, consulte [usar parâmetros &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md).  
  
## <a name="remarks"></a>Comentários  
 Atualmente, você pode enviar dados de várias linhas ao servidor como parâmetros para um procedimento com conjuntos de parâmetros (o parâmetro DBPARAMS em `ICommand::Execute`). Com conjuntos de parâmetros, todo elemento do conjunto tem que ser enviado ao servidor em uma solicitação RPC (chamada de procedimento remoto) separada. Os parâmetros com valor de tabela fornecem uma funcionalidade semelhante, mas interagem melhor com o servidor. Isso reduz o número de solicitações RPC e habilita operações baseadas em conjunto no servidor.  
  
 Os parâmetros com valor de tabela são suportados no provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client como objetos OLE DB `Rowset`. Qualquer objeto `Rowset` poderia ser fornecido pelo consumidor (ou seja, o aplicativo cliente usando o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client) como um espaço reservado para parâmetros com valor de tabela. Os parâmetros com valor de tabela são tratados como os outros tipos de parâmetro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client fornece interfaces de criação, descoberta, especificação, associação e de esquema.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Criação do conjunto de linhas do parâmetro com valor de tabela](table-valued-parameter-rowset-creation.md)  
  
-   [Descoberta do tipo de parâmetro com valor de tabela](../../database-engine/dev-guide/table-valued-parameter-type-discovery.md)  
  
-   [Executando comandos que contêm parâmetros com valor de tabela](executing-commands-containing-table-valued-parameters.md)  
  
-   [Inserindo dados em parâmetros com valor de tabela](inserting-data-into-table-valued-parameters.md)  
  
-   [Conjuntos de linhas de esquema alterados para parâmetros com valor de tabela de OLE DB](schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [Suporte ao tipo de parâmetro com valor de tabela OLE DB](ole-db-table-valued-parameter-type-support.md)  
  
-   [Suporte ao tipo de parâmetro com valor de tabela OLE DB &#40;Métodos&#41;](ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [Suporte ao tipo de parâmetro com valor de tabela do OLE DB &#40;Propriedades&#41;](ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
