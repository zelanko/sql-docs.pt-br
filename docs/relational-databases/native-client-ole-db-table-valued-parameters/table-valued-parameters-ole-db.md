---
title: Parâmetros com valor de tabela (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
ms.assetid: 4298b73d-615b-4d28-9843-03b4d5fc489e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 15055f582d7add6194753e2743d63b5e082318b5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300220"
---
# <a name="table-valued-parameters-ole-db"></a>Parâmetros com valor de tabela (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Esta seção descreve o suporte a parâmetros com valor de tabela no provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Para obter informações adicionais sobre a visão geral, consulte [Parâmetros de valor de tabela &#40;&#41;de cliente nativo do servidor SQL ](../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md). Para ver uma amostra, confira [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md).  
  
## <a name="remarks"></a>Comentários  
 Atualmente, você pode enviar dados de várias linhas ao servidor como parâmetros para um procedimento com conjuntos de parâmetros (o parâmetro DBPARAMS em **ICommand::Execute**). Com conjuntos de parâmetros, todo elemento do conjunto tem que ser enviado ao servidor em uma solicitação RPC (chamada de procedimento remoto) separada. Os parâmetros com valor de tabela fornecem uma funcionalidade semelhante, mas interagem melhor com o servidor. Isso reduz o número de solicitações RPC e habilita operações baseadas em conjunto no servidor.  
  
 Os parâmetros de valor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de tabela são suportados no Provedor OLE DB do Cliente Nativo como objetos OLE DB **Rowset.** Qualquer objeto **Rowset** pode ser fornecido pelo consumidor (ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja, o aplicativo cliente usando o Provedor OLE DB do Cliente Nativo) como um espaço reservado para parâmetros de parâmetros de parâmetros de valor de tabela. Os parâmetros com valor de tabela são tratados como os outros tipos de parâmetro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client fornece interfaces de criação, descoberta, especificação, associação e de esquema.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Criação do conjunto de linhas do parâmetro com valor de tabela](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)  
  
-   [Descoberta do tipo de parâmetro com valor de tabela](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md)  
  
-   [Executando comandos que contêm parâmetros com valor de tabela](../../relational-databases/native-client-ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md)  
  
-   [Inserindo dados em parâmetros com valor de tabela](../../relational-databases/native-client-ole-db-table-valued-parameters/inserting-data-into-table-valued-parameters.md)  
  
-   [Conjuntos de linhas de esquema alterados para parâmetros com valor de tabela de OLE DB](../../relational-databases/native-client-ole-db-table-valued-parameters/schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [Suporte ao tipo de parâmetro com valor de tabela OLE DB](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)  
  
-   [Suporte ao tipo de parâmetro com valor de tabela OLE DB &#40;Métodos&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [Suporte ao tipo de parâmetro com valor de tabela do OLE DB &#40;Propriedades&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Cliente nativo do servidor SQL &#40;o ledb&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
