---
title: Trabalhando com objetos de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- database objects [SMO]
- objects [SMO]
ms.assetid: 702fd63d-8734-4a02-872e-aecfb037c787
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d5190d6fcabe339d4d99e8b5001174c9f638b54a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48148246"
---
# <a name="working-with-database-objects"></a>Trabalhando com objetos de banco de dados
  As fases da criação de objetos SMO são as seguintes:  
  
1.  Criar uma instância do objeto.  
  
2.  Definir as propriedades do objeto.  
  
3.  Criar instâncias dos objetos filhos.  
  
4.  Definir as propriedades dos objetos filhos.  
  
5.  Criar o objeto.  
  
 Quando são criadas instâncias de objetos SMO em um aplicativo SMO, elas não existem na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] até que o método `Create` seja emitido. Porém, não é necessário emitir um método `Create` para cada objeto individual. Se um objeto tiver um conjunto de objetos filhos, apenas o objeto pai será necessário para executar o método `Create`. Por exemplo, a definição de uma tabela exige que ela contenha pelo menos uma coluna para existir. Além disso, uma coluna não pode existir em isolamento sem uma tabela. Há uma relação codependente entre a tabela e suas colunas.  
  
 O método <xref:Microsoft.SqlServer.Management.Dmf.Policy.Alter%2A> permite fazer alterações a um objeto. Várias alterações a um objeto, como a adição de objetos filhos a uma das coleções do objeto ou a alteração de um valor de propriedade, são colocados em lotes e executados de uma vez. O método `Alter` reduz o tráfego de rede e aprimora o desempenho geral.  
  
 A instrução `Drop` é usada para remover um objeto e todos os seus objetos filhos codependentes que foram necessário para criar o objeto inicialmente.  
  
## <a name="see-also"></a>Consulte também  
 [Modelo de objeto SMO](../smo-object-model.md)  
  
  
