---
title: Remover chamadas para o comando DBCC CONCURRENCYVIOLATION preterido | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2cc9f6ff-de36-4e94-bd04-59f5c45c4911
caps.latest.revision: 7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2486546efae7daa63441e12fa350ef878c7daa77
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37261892"
---
# <a name="remove-calls-to-the-deprecated-dbcc-concurrencyviolation-command"></a>Remover chamadas ao comando obsoleto DBCC CONCURRENCYVIOLATION
  O Supervisor de Atualização detectou o uso do comando DBCC CONCURRENCYVIOLATION. Este comando não está mais disponível. A execução desse comando retorna o erro 2526.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 Nenhuma versão recente da edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui um administrador de carga de trabalho, por isso o comando foi removido.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Atualize os aplicativos e scripts para remover referências a esse comando obsoleto.  
  
## <a name="external-resources"></a>Recursos externos  
  
