---
title: Salvar resultados de rastreamento em um arquivo
titleSuffix: SQL Server Profiler
description: Descubra como salvar dados de eventos capturados em um arquivo de rastreamento, especifique um tamanho máximo de arquivo de rastreamento e habilite a opção de sobreposição de arquivo no SQL Server Profiler.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: ac528747-0c19-4f3d-96f5-44c762a4abed
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: f792be448dc9e11ce4245e7dd5cda08d9d750c2b
ms.sourcegitcommit: b8933ce09d0e631d1183a84d2c2ad3dfd0602180
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83151702"
---
# <a name="save-trace-results-to-a-file-sql-server-profiler"></a>Salvar resultados de rastreamento em um arquivo (SQL Server Profiler)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este tópico descreve como salvar resultados de rastreamento em um arquivo, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-save-trace-results-to-a-file"></a>Para salvar resultados de rastreamento em um arquivo  
  
1.  No menu **Arquivo** , clique em **Novo Rastreamento**e conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     A caixa de diálogo **Propriedades do Rastreamento**é exibida.  
  
    > [!NOTE]  
    >  Se **Iniciar rastreamento imediatamente após estabelecer a conexão**estiver selecionado, a caixa de diálogo **Propriedades do Rastreamento**não será exibida e o rastreamento será iniciado. Para desabilitar essa configuração, no menu **Ferramentas**, clique em **Opções**e desmarque a caixa de seleção **Iniciar rastreamento imediatamente após estabelecer a conexão** .  
  
2.  Na caixa **Nome do rastreamento** , digite um nome para o rastreamento.  
  
3.  Marque a caixa de seleção **Salvar em arquivo** .  
  
     A caixa de diálogo **Salvar Como**é exibida.  
  
4.  Especifique um caminho e um nome de arquivo, na caixa de diálogo **Salvar Como**. Clique em **Salvar.**  
  
    > [!NOTE]  
    >  Certifique-se de que o serviço do SQL Server tenha permissões adequadas para gravação em arquivo no diretório especificado.  
  
5.  Na caixa de diálogo **Propriedades do Rastreamento** , insira o tamanho do arquivo máximo na caixa de texto **Definir tamanho máximo do arquivo (MB)** . O valor padrão é 5 megabytes (MB).  
  
6.  Opcionalmente, especifique as seguintes opções:  
  
    -   Marque a caixa de seleção **Habilitar substituição de arquivo** para que o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] crie novos arquivos para rastreamento de dados quando o tamanho máximo for atingido. Esta opção é selecionada por padrão.  
  
    -   Marque a caixa de seleção **Dados de rastreamento de processos do servidor** para assegurar que o servidor registre cada evento de rastreamento.  
  
        > [!NOTE]  
        >  Quando a opção **Dados de rastreamento de processos do servidor**está desmarcada, o servidor não registrará eventos caso eles degradem significativamente o desempenho.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
