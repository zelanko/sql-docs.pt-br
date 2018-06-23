---
title: Sobre propriedades OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, properties
- SQL Server Native Client OLE DB provider, properties
- properties [OLE DB]
- property values [SQL Server Native Client]
ms.assetid: 0b36a61e-b542-400d-a3d2-e6f643caf2c6
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b962ccf3212f8bfd1179b7c3b8c8219d968ca734
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119326"
---
# <a name="about-ole-db-properties"></a>Sobre propriedades OLE DB
  Os consumidores definem valores de propriedade para solicitar um comportamento de objeto específico. Por exemplo, os consumidores usam propriedades para especificar as interfaces a serem expostas por um conjunto de linhas. Eles obtêm os valores de propriedade para determinar os recursos de um objeto, como um conjunto de linhas, uma sessão ou um objeto de fonte de dados.  
  
 Cada propriedade tem um valor, um tipo, uma descrição e um atributo de leitura/gravação e, no caso de propriedades de conjunto de linhas, um indicador que determina se ela pode ser aplicada por coluna.  
  
 Uma propriedade é identificada por um GUID e um inteiro que representam a ID de propriedade. Um conjunto de propriedades é um conjunto de todas as propriedades que compartilham o mesmo GUID. Além de propriedade predefinida do OLE DB define, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client implementa propriedades e conjuntos de propriedades específicas do provedor neles. Cada propriedade pertence a um ou mais grupos de propriedades. Um grupo de propriedades é o grupo de todas as propriedades que se aplicam a um objeto específico. Alguns grupos de propriedades incluem o grupo de propriedades de inicialização, o grupo de propriedades de fonte de dados, o grupo de propriedades de sessão, o grupo de propriedades de conjunto de linhas, o grupo de propriedades de tabela e o grupo de propriedades de coluna. Há propriedades em cada um desses grupos de propriedade.  
  
 A definição dos valores de propriedade envolve:  
  
1.  Determinar as propriedades para as quais definir valores.  
  
2.  Determinar os conjuntos de propriedades que contêm as propriedades identificadas.  
  
3.  Alocar uma matriz de estruturas DBPROPSET, uma para cada conjunto de propriedades identificadas.  
  
4.  Alocar uma matriz de estruturas DBPROP para cada conjunto de propriedades. O número de elementos em cada matriz é o número de propriedades (identificadas na Etapa 1) que pertencem ao conjunto de propriedades.  
  
5.  Preencher a estrutura DBPROP para cada propriedade.  
  
6.  Preencher as informações (GUID do conjunto de propriedades, contagem do número de elementos e um ponteiro para a matriz DBPROP correspondente) na estrutura DBPROPSET para cada conjunto de propriedades.  
  
7.  Chamar um método para definir propriedades e passar a contagem e a matriz de estruturas DBPROPSET.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um aplicativo de provedor do SQL Server Native Client OLE DB](creating-a-sql-server-native-client-ole-db-provider-application.md)   
 [Propriedades (OLE DB)](http://go.microsoft.com/fwlink/?LinkId=112207)  
  
  