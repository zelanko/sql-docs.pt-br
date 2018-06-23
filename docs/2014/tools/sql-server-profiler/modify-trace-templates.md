---
title: Modificar modelos de rastreamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- templates [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler], templates
- trace templates [SQL Server]
- modifying trace templates
- SQL Server Profiler, templates
ms.assetid: 75b62a54-8d16-4599-bd2d-c42cfcc209f4
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 08c08bd8838380ce1054e13697aa6873a8e98860
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130886"
---
# <a name="modify-trace-templates"></a>Modificar modelos de rastreamento
  Você pode modificar os modelos salvos em um arquivo no computador local em que é executado o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] . Você também pode modificar modelos derivados desses arquivos. Ao modificar modelos existentes, edite as propriedades do modelo, como classes de evento e colunas de dados, na mesma ordem em que essas propriedades foram definidas originalmente, na guia **Seleção de Eventos** da caixa de diálogo **Propriedades do Rastreamento** . As classes de evento e colunas de dados podem ser adicionadas ou removidas e os filtros podem ser alterados. Depois que o modelo é modificado, um modelo específico ao usuário é criado, mantendo-se intacto o modelo do sistema original. Para obter mais informações, veja [Salvar rastreamentos e modelos de rastreamento](save-traces-and-trace-templates.md).  
  
 Talvez seja necessário derivar um modelo de um arquivo de rastreamento, caso você não consiga se lembrar do modelo original usado para criar o rastreamento (ou não o tenha salvado) ou se desejar executar o mesmo rastreamento em data futura. Ao trabalhar com rastreamentos existentes, você pode exibir as propriedades, mas não pode modificá-las. Para modificar as propriedades, interrompa ou pause o rastreamento. Para obter mais informações, veja [Derivar um modelo com base em um arquivo ou uma tabela de rastreamento &#40;SQL Server Profiler&#41;](sql-server-profiler.md) e [Derivar um modelo de um rastreamento em execução &#40;SQL Server Profiler&#41;](derive-a-template-from-a-running-trace-sql-server-profiler.md).  
  
 **Para criar um modelo de rastreamento**  
  
 [Criar um modelo de rastreamento &#40;SQL Server Profiler&#41;](create-a-trace-template-sql-server-profiler.md)  
  
 **Para executar um rastreamento a partir de um modelo de rastreamento**  
  
 [Criar um rastreamento &#40;SQL Server Profiler&#41;](create-a-trace-sql-server-profiler.md)  
  
 **Para modificar um modelo de rastreamento**  
  
 [Usando o SQL Server Profiler](../../database-engine/modify-a-trace-template-sql-server-profiler.md)  
  
 [Usando Transact-SQL](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md)  
  
 **Para adicionar ou remover eventos de um modelo ou arquivo de rastreamento**  
  
 [Usando o SQL Server Profiler](specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
 [Usando Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar um rastreamento](start-a-trace.md)  
  
  
