---
title: 'Lição 3: Usando o utilitário de Prompt de comando dta | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 30f27f4d-8852-4b12-ba62-57f63e496f1d
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 086a2051f5ef1900c90e55c2de21d365b24905d7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33070163"
---
# <a name="lesson-3-using-the-dta-command-prompt-utility"></a>Lição 3: Usando o utilitário de prompt de comando dta
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
O utilitário de prompt de comando **dta** oferece funcionalidade além da fornecida pelo Orientador de Otimização do Mecanismo de Banco de Dados.  
  
Você pode usar suas ferramentas XML favoritas para criar arquivos de entrada para o utilitário usando o esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados. Esse esquema é instalado durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e pode ser encontrado em: C:\Arquivos de Programas (x86)\Microsoft SQL Server\110\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd.  
  
O esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados também está disponível online no [Microsoft Web site](http://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409).  
  
O esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados oferece mais flexibilidade para definir opções de ajuste. Ele permite, por exemplo, executar a análise hipotética. A análise hipotética compreende a especificação de um conjunto de estruturas de design físicas hipotéticas e existentes para o banco de dados a ser ajustado e a análise usando o Orientador de Otimização do Mecanismo de Banco de Dados para descobrir se esse design físico hipotético melhorará o desempenho do processamento de consulta. Esse tipo de análise oferece a vantagem de poder avaliar a nova configuração sem incorrer na sobrecarga da implementação de fato. Se seu design físico hipotético não oferecer a melhora de desempenho desejada, é fácil alterá-lo e fazer novas análises até que você alcance a configuração que produza os resultados necessários.  
  
Além disso, usando o esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados e o utilitário de prompt de comando **dta** , você pode inserir a funcionalidade do Orientador de Otimização do Mecanismo de Banco de Dados em scripts e usá-la com outras ferramentas de design de banco de dados.  
  
A utilização da funcionalidade de entrada XML do Orientador de Otimização do Mecanismo de Banco de Dados ultrapassa o alcance desta lição.  
  
Esta lição fornece uma introdução à sintaxe básica do utilitário de prompt de comando **dta** , como acessar a ajuda e à prática do ajuste de cargas de trabalho simples.  
  
Ela contém o seguinte tópico:  
  
-   Iniciando o utilitário de prompt de comando **dta** e ajustando uma carga de trabalho  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Iniciando o utilitário de prompt de comando dta e ajustando uma carga de trabalho](../../tools/dta/lesson-3-1-starting-the-dta-command-prompt-utility-and-tuning-a-workload.md)  
  
  
  
