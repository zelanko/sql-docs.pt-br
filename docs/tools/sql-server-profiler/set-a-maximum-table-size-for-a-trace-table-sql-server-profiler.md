---
title: Definir um tamanho máximo para uma tabela de rastreamento
titleSuffix: SQL Server Profiler
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: d0ae83e5-1c88-4a2e-be05-2c341280b978
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 21d68638d85acd48f8f1c552319b0ea4784dec68
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75307610"
---
# <a name="set-a-maximum-table-size-for-a-trace-table-sql-server-profiler"></a>Definir um tamanho máximo para uma tabela de rastreamento (SQL Server Profiler)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este tópico descreve como definir um tamanho máximo para tabelas de rastreamento usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-set-a-maximum-table-size-for-a-trace-table"></a>Para definir um tamanho máximo para uma tabela de rastreamento  
  
1.  No menu **Arquivo** , clique em **Novo Rastreamento**e conecte a uma instância do SQL Server.  
  
     A caixa de diálogo **Propriedades do Rastreamento**é exibida.  
  
    > [!NOTE]  
    >  Se **Iniciar rastreamento imediatamente após estabelecer a conexão**estiver selecionado, a caixa de diálogo **Propriedades do Rastreamento**não será exibida e o rastreamento será iniciado. Para desabilitar essa configuração, no menu **Ferramentas**, clique em **Opções**e desmarque a caixa de seleção **Iniciar rastreamento imediatamente após estabelecer a conexão** .  
  
2.  Na caixa **Nome do rastreamento** , digite um nome para o rastreamento.  
  
3.  Na lista **Nome do modelo**, selecione um modelo de rastreamento.  
  
4.  Marque a caixa de seleção **Salvar em tabela**.  
  
5.  Conecte-se ao servidor em que deseja armazenar o rastreamento.  
  
     A caixa de diálogo **Tabela de Destino** é exibida.  
  
6.  Selecione um banco de dados para o rastreamento na lista **Banco de Dados** .  
  
7.  Na caixa **Tabela** , digite ou selecione um nome de tabela.  
  
8.  Marque a caixa de seleção **Definir máximo de linhas** e especifique um número máximo de linhas para a tabela de rastreamento.  
  
    > [!NOTE]  
    >  Quando o número de linhas na tabela exceder o máximo especificado, os eventos do rastreamento deixarão de ser registrados. O rastreamento, porém, continuará.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
