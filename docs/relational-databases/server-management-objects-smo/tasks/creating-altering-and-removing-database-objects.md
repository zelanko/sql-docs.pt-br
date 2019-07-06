---
title: Trabalhando com objetos de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- database objects [SMO]
- objects [SMO]
ms.assetid: 702fd63d-8734-4a02-872e-aecfb037c787
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c79ccb4805030cb93e67fa335e72de4d5984a62a
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67583570"
---
# <a name="creating-altering-and-removing-database-objects"></a>Criar, alterar e remover objetos de bancos de dados
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  As fases da criação de objetos SMO são as seguintes:  
  
1.  Criar uma instância do objeto.  
  
2.  Definir as propriedades do objeto.  
  
3.  Criar instâncias dos objetos filhos.  
  
4.  Definir as propriedades dos objetos filhos.  
  
5.  Criar o objeto.  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 Quando são criadas instâncias de objetos SMO em um aplicativo SMO, elas não existem na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] até que o método **Create** seja emitido. Porém, não é necessário emitir um método **Create** para cada objeto individual. Se um objeto tiver um conjunto de objetos filhos, apenas o objeto pai será necessário para executar o método **Create** . Por exemplo, a definição de uma tabela exige que ela contenha pelo menos uma coluna para existir. Além disso, uma coluna não pode existir em isolamento sem uma tabela. Há uma relação codependente entre a tabela e suas colunas.  
  
 O método <xref:Microsoft.SqlServer.Management.Dmf.Policy.Alter%2A> permite fazer alterações a um objeto. Várias alterações a um objeto, como a adição de objetos filhos a uma das coleções do objeto ou a alteração de um valor de propriedade, são colocados em lotes e executados de uma vez. O método **Alter** reduz o tráfego de rede e aprimora o desempenho geral.  
  
 A instrução **Drop** é usada para remover um objeto e todos os seus objetos filhos codependentes que foram necessário para criar o objeto inicialmente.  
  
## <a name="see-also"></a>Consulte também  
 [Modelo de objeto SMO](../../../relational-databases/server-management-objects-smo/smo-object-model.md)  
  
  
