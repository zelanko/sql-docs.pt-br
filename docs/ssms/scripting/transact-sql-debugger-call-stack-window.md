---
title: Janela Pilha de Chamadas
description: Saiba como usar a Janela Pilha de Chamadas do depurador Transact-SQL para ver tipos de dados de parâmetro e também valores de procedimentos armazenados, funções e gatilhos.
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- Call Stack Window [Transact-SQL]
ms.assetid: ddb0b19c-87cd-4883-bcb8-ec09ffb30369
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8421e448b36cb1cf4958ef5cfaa1d583a7cca262
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248011"
---
# <a name="transact-sql-debugger---call-stack-window"></a>Depurador do Transact-SQL – Janela Pilha de Chamadas

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

A janela **Pilha de Chamadas** exibe os módulos da pilha de chamadas e os valores e tipos de dados de quaisquer parâmetros que passaram para os módulos. [!INCLUDE[tsql](../../includes/tsql-md.md)] os módulos incluem procedimentos armazenados, funções e gatilhos. Para exibir a pilha de chamadas, você deve estar no modo de depuração.  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>Lista de Tarefas

**Para acessar a janela Pilha de Chamadas**

- No menu **Depurar** , clique em **Janelas**e em **Pilha de Chamadas**.

**Para alterar o quadro atual da Pilha de Chamadas**

Você pode usar qualquer um dos seguintes procedimentos para montar o quadro atual do quadro de pilhas:

- Clique com o botão direito do mouse no registro de ativação e depois clique em **Alternar para Quadro**.

- Clique duas vezes no quadro de pilhas.  

**Para exibir a origem de um quadro diferente do quadro atual**

- Clique com o botão direito do mouse no registro de ativação e depois clique em **Ir para Código-Fonte**.

## <a name="stack-frames"></a>Quadros de pilhas

Cada linha na janela **Pilha de Chamadas** é chamada de um registro de ativação e representa a chamada de um módulo de um arquivo de script [!INCLUDE[tsql](../../includes/tsql-md.md)] ou uma chamada de um módulo a outro. O registro de ativação inferior no vídeo indica a linha da janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que fez a primeira chamada na pilha. A linha superior indica em qual linha o depurador pausou a depuração e é identificada por uma seta amarela na margem esquerda da janela. Cada linha intermediária indica o módulo e o número de linha do código fonte que chamou o próximo quadro de pilha mais alto.  

Todas as expressões nas janelas **Locais**, **Inspecionar**e **QuickWatch** são avaliadas com base no registro de ativação atual. A janela Editor de Consultas exibe o código para o quadro atual. Por padrão, o registro de ativação atual é o quadro no qual o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] pausou a execução. Quando você altera o registro de ativação atual para outro quadro, as expressão das janelas **Locais**, **Inspecionar**e **QuickWatch** são reavaliadas no contexto do novo quadro de pilhas e o código-fonte do novo quadro é exibido na janela Editor de Consultas.  
  
## <a name="columns"></a>Colunas

 **Nome**  
 Exibe informações sobre um módulo na pilha de chamadas.  
  
 Na linha inferior da pilha de chamadas, **Nome** relaciona a janela de fonte do Editor de Consultas e o número de linha que fez a primeira chamada na pilha. Para as outras linhas, **Nome** apresenta o formato **Module(Instance.Database)(ParmList) LineNumber**.  
  
 **Módulo**  
 É o nome do procedimento armazenado, função ou procedimento armazenado que chamou o próximo quadro.  
  
 **Instance.Database**  
 É a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e do banco de dados que está segurando o módulo.  
  
 **ParmList**  
 Indica o tipo de dados, o nome e o valor de cada parâmetro transmitido dentro durante a chamada para o módulo.  
  
 **LineNumber**  
 Para todas as linhas excluindo a linha de parte superior, **LineNumber** indica qual linha no módulo chamou o quadro. Para a linha de parte superior, **LineNumber** indica a linha na qual o depurador está atualmente focalizado.  
  
 **Idioma**  
 Exibe **Transact-SQL** para [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="see-also"></a>Consulte Também

- [Depurador do Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)
- [Informações do depurador Transact-SQL](../../relational-databases/scripting/transact-sql-debugger-information.md)
- [Percorrer o código do Transact-SQL](../../relational-databases/scripting/step-through-transact-sql-code.md)
