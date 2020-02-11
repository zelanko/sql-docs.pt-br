---
title: 'Lição 3: Como usar o utilitário de Prompt de comando dta | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 30f27f4d-8852-4b12-ba62-57f63e496f1d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e2881a2a118306f9d567236516f05bb29ad2d60a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68186569"
---
# <a name="lesson-3-using-the-dta-command-prompt-utility"></a>Lição 3: Usando o utilitário de prompt de comando dta
  O utilitário de prompt de comando **DTA** oferece funcionalidade além da fornecida pelo Orientador de otimização do mecanismo de banco de dados.  
  
 Você pode usar suas ferramentas XML favoritas para criar arquivos de entrada para o utilitário usando o esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados. Esse esquema é instalado durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e pode ser encontrado em: C:\Arquivos de Programas (x86)\Microsoft SQL Server\110\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd.  
  
 O esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados também está disponível online no [Microsoft Web site](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409).  
  
 O esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados oferece mais flexibilidade para definir opções de ajuste. Ele permite, por exemplo, executar a análise hipotética. A análise hipotética compreende a especificação de um conjunto de estruturas de design físicas hipotéticas e existentes para o banco de dados a ser ajustado e a análise usando o Orientador de Otimização do Mecanismo de Banco de Dados para descobrir se esse design físico hipotético melhorará o desempenho do processamento de consulta. Esse tipo de análise oferece a vantagem de poder avaliar a nova configuração sem incorrer na sobrecarga da implementação de fato. Se seu design físico hipotético não oferecer a melhora de desempenho desejada, é fácil alterá-lo e fazer novas análises até que você alcance a configuração que produza os resultados necessários.  
  
 Além disso, usando o esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados e o utilitário de prompt de comando **dta** , você pode inserir a funcionalidade do Orientador de Otimização do Mecanismo de Banco de Dados em scripts e usá-la com outras ferramentas de design de banco de dados.  
  
 A utilização da funcionalidade de entrada XML do Orientador de Otimização do Mecanismo de Banco de Dados ultrapassa o alcance desta lição.  
  
 Esta lição fornece uma introdução à sintaxe básica do utilitário de prompt de comando **dta** , como acessar a ajuda e à prática do ajuste de cargas de trabalho simples.  
  
 Ela contém o seguinte tópico:  
  
-   Iniciando o utilitário de prompt de comando **DTA** e ajustando uma carga de trabalho  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Iniciando o utilitário de prompt de comando dta e ajustando uma carga de trabalho](lesson-1-1-tuning-a-workload.md)  
  
  
