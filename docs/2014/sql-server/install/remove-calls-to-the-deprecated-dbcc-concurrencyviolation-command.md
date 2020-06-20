---
title: Remover chamadas para o comando de DBCC CONCURRENCYVIOLATION preterido | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2cc9f6ff-de36-4e94-bd04-59f5c45c4911
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: cde04ebfc2ea9996d1c9ed233123e5b66f6e81fa
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065207"
---
# <a name="remove-calls-to-the-deprecated-dbcc-concurrencyviolation-command"></a>Remover chamadas ao comando obsoleto DBCC CONCURRENCYVIOLATION
  O Supervisor de Atualização detectou o uso do comando DBCC CONCURRENCYVIOLATION. Este comando não está mais disponível. A execução desse comando retorna o erro 2526.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrição  
 Nenhuma versão recente da edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui um administrador de carga de trabalho, por isso o comando foi removido.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Atualize os aplicativos e scripts para remover referências a esse comando obsoleto.  
  
## <a name="external-resources"></a>Recursos externos  
  
