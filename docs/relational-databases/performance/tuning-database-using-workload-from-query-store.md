---
title: "Ajustando o banco de dados usando a carga de trabalho do repositório de consultas | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Database Engine Tuning Advisor, Query Store
ms.assetid: 17107549-5073-4fa2-8ee7-5ed33b38821e
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7f89ed5e87b8fd51e8618a8559679225d91b32de
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="tuning-database-using-workload-from-query-store"></a>Ajustando o banco de dados usando a carga de trabalho do repositório de consulta
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]


O recurso [Repositório de Consultas](../../relational-databases/performance/how-query-store-collects-data.md) no SQL Server captura automaticamente um histórico das consultas, planos e estatísticas de tempo de execução e persiste essas informações no banco de dados. O [DTA (Orientador de Otimização do Mecanismo de Banco de Dados)](../../relational-databases/performance/database-engine-tuning-advisor.md) dá suporte a uma nova opção para usar o armazenamento de consulta para selecionar automaticamente uma carga de trabalho adequada para ajuste. Para muitos usuários, isso pode eliminar a necessidade de coletar explicitamente uma carga de trabalho para ajuste. Esse recurso só estará disponível se o banco de dados tiver o recurso Repositório de Consultas ativado. 
  
  Esse recurso está disponível no SQL Server Management Studio versão **16.4** ou superior. 
  
<a name="how-to-tune-a-workload-from-query-store-in-database-engine-tuning-advisor-gui"></a>Como ajustar uma carga de trabalho do repositório de consulta na GUI do Orientador de otimização do mecanismo de banco de dados
---
No GUI do DTA, selecione o botão de opção **Repositório de Consultas** no painel **Geral** para habilitar esse recurso (veja a figura abaixo).
![Carga de trabalho do DTA do repositório de consultas](../../relational-databases/performance/media/dta-workload-from-query-store.gif)
 
<a name="how-to-tune-a-workload-from-query-store-in-dtaexe-command-line-utility"></a>Como ajustar uma carga de trabalho do repositório de consulta no utilitário de linha de comando do dta.exe
---
Na linha de comando (dta.exe), escolha a opção **-iq** para selecionar a carga de trabalho do Repositório de Consulta. 

Há duas opções adicionais disponíveis por meio da linha de comando que ajuda a ajustar o comportamento do DTA ao selecionar a carga de trabalho no Repositório de Consultas. Essas opções não estão disponíveis por meio do GUI:
  1. Número de eventos de carga de trabalho a ajustar: essa opção, especificada usando a linha de comando **-n**, permite ao usuário controlar quantos eventos do Repositório de Consultas são ajustados. Por padrão, o DTA usa um valor de 1000 para essa opção. Observe que o DTA sempre escolhe os eventos mais caros por duração total. 
  
  2. Janelas de tempo dos eventos a serem ajustados: como o Repositório de Consultas pode conter consultas que foram executadas há muito tempo, essa opção permite que o usuário especifique uma janela de tempo anterior (em horas) de quando uma consulta deve ter sido executado para que ela seja considerada pelo DTA para ajuste. Essa opção é especificada usando o argumento de linha de comando **-I**. 

Consulte [Utilitário dta](../../tools/dta/dta-utility.md) para obter mais informações.

<a name="difference-between-using-workload-from-query-store-and-plan-cache"></a>Diferença entre usar a carga de trabalho do Repositório de Consultas e do Cache de Planos 
--- 
A diferença entre as opções de Repositório de Consultas e de Cache de Planos é que o primeiro contém um histórico maior de consultas que foram executadas no banco de dados, persistidas entre as reinicializações do servidor. Por outro lado, o Cache de Planos contém apenas um subconjunto de consultas recém-executadas cujos planos são armazenados em cache na memória. Quando o servidor for reiniciado, as entradas no Cache de Planos serão descartadas.

<a name="see-also"></a>Consulte também 
--- 
[Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/database-engine-tuning-advisor.md)     
[Tutorial: Orientador de Otimização do Mecanismo de Banco de Dados](Tutorial:%20Database%20Engine%20Tuning%20Advisor.md)     
[Como o Repositório de Consultas coleta dados](../../relational-databases/performance/how-query-store-collects-data.md)     
[Práticas recomendadas do Repositório de Consultas](../../relational-databases/performance/best-practice-with-the-query-store.md)

