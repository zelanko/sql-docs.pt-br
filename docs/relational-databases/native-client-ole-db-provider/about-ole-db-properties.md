---
title: Sobre propriedades OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, properties
- SQL Server Native Client OLE DB provider, properties
- properties [OLE DB]
- property values [SQL Server Native Client]
ms.assetid: 0b36a61e-b542-400d-a3d2-e6f643caf2c6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e2b07f78cedc95e39b2268b56c9690cdb9c063f0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81289659"
---
# <a name="about-ole-db-properties"></a>Sobre propriedades OLE DB
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Os consumidores definem valores de propriedade para solicitar um comportamento de objeto específico. Por exemplo, os consumidores usam propriedades para especificar as interfaces a serem expostas por um conjunto de linhas. Eles obtêm os valores de propriedade para determinar os recursos de um objeto, como um conjunto de linhas, uma sessão ou um objeto de fonte de dados.  
  
 Cada propriedade tem um valor, um tipo, uma descrição e um atributo de leitura/gravação e, no caso de propriedades de conjunto de linhas, um indicador que determina se ela pode ser aplicada por coluna.  
  
 Uma propriedade é identificada por um GUID e um inteiro que representam a ID de propriedade. Um conjunto de propriedades é um conjunto de todas as propriedades que compartilham o mesmo GUID. Além dos conjuntos de propriedades predefinidos OLE DB, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o provedor de OLE DB de cliente nativo implementa as propriedades e os conjuntos de propriedade específicos do provedor neles. Cada propriedade pertence a um ou mais grupos de propriedades. Um grupo de propriedades é o grupo de todas as propriedades que se aplicam a um objeto específico. Alguns grupos de propriedades incluem o grupo de propriedades de inicialização, o grupo de propriedades de fonte de dados, o grupo de propriedades de sessão, o grupo de propriedades de conjunto de linhas, o grupo de propriedades de tabela e o grupo de propriedades de coluna. Há propriedades em cada um desses grupos de propriedade.  
  
 A definição dos valores de propriedade envolve:  
  
1.  Determinar as propriedades para as quais definir valores.  
  
2.  Determinar os conjuntos de propriedades que contêm as propriedades identificadas.  
  
3.  Alocar uma matriz de estruturas DBPROPSET, uma para cada conjunto de propriedades identificadas.  
  
4.  Alocar uma matriz de estruturas DBPROP para cada conjunto de propriedades. O número de elementos em cada matriz é o número de propriedades (identificadas na Etapa 1) que pertencem ao conjunto de propriedades.  
  
5.  Preencher a estrutura DBPROP para cada propriedade.  
  
6.  Preencher as informações (GUID do conjunto de propriedades, contagem do número de elementos e um ponteiro para a matriz DBPROP correspondente) na estrutura DBPROPSET para cada conjunto de propriedades.  
  
7.  Chamar um método para definir propriedades e passar a contagem e a matriz de estruturas DBPROPSET.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando um aplicativo de provedor de OLE DB de SQL Server Native Client](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)   
 [Propriedades (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=112207)  
  
  
