---
title: Remover UDT&#39;s nomeados após o tipo de dados ORDPATH reservado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 474e910a-6abb-4e28-acc2-055338c011d4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3ee155c70a8b10d4437d6b2f374c8b9497bf3faa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66092917"
---
# <a name="remove-udt39s-named-after-the-reserved-ordpath-data-type"></a>Remover UDT&#39;s nomeados após o tipo de dados ORDPATH reservado
  O Supervisor de Atualização detectou um tipo definido pelo usuário (UDT) que tem o mesmo nome de um termo reservado para o tipo de dados `ORDPATH`.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>DESCRIÇÃO  
 Os termos usados para tipos de dados internos não devem ser utilizados como nomes de UDTs de alias ou CLR.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Remova o UDT que tem o mesmo nome do tipo de dados e recrie o UDT com um nome não reservado.  
  
## <a name="external-resources"></a>Recursos externos  
 [Criar um tipo definido pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
