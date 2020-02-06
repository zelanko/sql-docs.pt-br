---
title: Salvar resultados de rastreamento em uma tabela
titleSuffix: SQL Server Profiler
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: edbecf74-683b-4e43-a1ef-7a3d5f5e27f6
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 6fb406988c9aeb92e7f0c1d3689e5b513a7ea0d3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75307430"
---
# <a name="save-trace-results-to-a-table-sql-server-profiler"></a>Salvar resultados de rastreamento em uma tabela (SQL Server Profiler)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este tópico descreve como salvar resultados de rastreamento em uma tabela do banco de dados, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
## <a name="to-save-trace-results-to-a-table"></a>Para salvar resultados de rastreamento em uma tabela
  
1.  No menu **Arquivo** , clique em **Novo Rastreamento**e conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     A caixa de diálogo **Propriedades do Rastreamento**é exibida.  
  
    > [!NOTE]  
    >  Se **Iniciar rastreamento imediatamente após estabelecer a conexão**estiver selecionado, a caixa de diálogo **Propriedades do Rastreamento**não será exibida e o rastreamento será iniciado. Para desabilitar essa configuração, no menu **Ferramentas**, clique em **Opções**e desmarque a caixa de seleção **Iniciar rastreamento imediatamente após estabelecer a conexão** .  
  
2.  Na caixa de diálogo **Nome do rastreamento** , digite um nome para o rastreamento e clique em **Salvar em tabela**.  
  
3.  Na caixa de diálogo **Conectar ao Servidor** , conecte-se ao banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que conterá a tabela de rastreamento.  
  
4.  Na caixa de diálogo **Tabela de Destino** , selecione um banco de dados na lista **Banco de Dados**.  
  
5.  Na lista **Proprietário** , selecione o proprietário do rastreamento.  
  
6.  Na lista **Tabela** , digite ou selecione o nome da tabela a conter os resultados do rastreamento. Clique em **OK.**  
  
7.  Na caixa de diálogo **Propriedades do Rastreamento** , marque a caixa de seleção **Definir máximo de linhas (em milhares)** para especificar o número máximo de linhas a serem salvas.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
