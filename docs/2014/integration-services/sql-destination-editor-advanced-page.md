---
title: Editor de destino SQL (página Avançado) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlserverdestadapter.advanced.f1
helpviewer_keywords:
- SQL Server Destination Editor
ms.assetid: 9b46bcf8-ddaf-4d7d-90a6-80bc19517e9b
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a70bcc9e853908022147ef02e9d2019179c90875
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52545493"
---
# <a name="sql-destination-editor-advanced-page"></a>Editor de Destino SQL (página Avançado)
  Use a página **Avançado** da caixa de diálogo **Editor de Destino SQL** para especificar opções avançadas de inserção em massa.  
  
 Para obter mais informações sobre destino do SQL Server, consulte [SQL Server Destination](data-flow/sql-server-destination.md).  
  
## <a name="options"></a>Opções  
 **Manter identidade**  
 Especifique se a tarefa deve inserir valores em colunas de identidade. O valor padrão dessa propriedade é `False`.  
  
 **Manter nulos**  
 Especifique se a tarefa deve manter valores nulos. O valor padrão dessa propriedade é `False`.  
  
 **Bloqueio de tabela**  
 Especifique se a tabela deve ser bloqueada no carregamento de dados. O valor padrão dessa propriedade é `True`.  
  
 **Verificar restrições**  
 Especifique se a tarefa deve verificar restrições. O valor padrão dessa propriedade é `True`.  
  
 **Acionadores**  
 Especifique se a inserção em massa deve ativar gatilhos em tabelas. O valor padrão dessa propriedade é `False`.  
  
 **Primeira Linha**  
 Especifique a primeira linha a inserir. O valor padrão desta propriedade é **-1**, indicando que nenhum valor foi atribuído.  
  
> [!NOTE]  
>  Limpe a caixa de texto no **Editor de Destino SQL** para indicar que não deseja atribuir um valor para esta propriedade. Use -1 na janela **Propriedades** , no **Editor Avançado**e no modelo de objeto.  
  
 **Última Linha**  
 Especifique a última linha a inserir. O valor padrão desta propriedade é **-1**, indicando que nenhum valor foi atribuído.  
  
> [!NOTE]  
>  Limpe a caixa de texto no **Editor de Destino SQL** para indicar que não deseja atribuir um valor para esta propriedade. Use -1 na janela **Propriedades** , no **Editor Avançado**e no modelo de objeto.  
  
 **Número máximo de erros**  
 Especifique o número máximo de erros permitido antes que a inserção em massa cesse. O valor padrão desta propriedade é **-1**, indicando que nenhum valor foi atribuído.  
  
> [!NOTE]  
>  Limpe a caixa de texto no **Editor de Destino SQL** para indicar que não deseja atribuir um valor para esta propriedade. Use -1 na janela **Propriedades** , no **Editor Avançado**e no modelo de objeto.  
  
 **Tempo Limite**  
 Especifique o tempo limite, em segundos, a ser aguardado antes de interrupção da inserção em massa.  
  
 **Ordenar colunas**  
 Digite os nomes das colunas de classificação. Cada coluna pode ser classificada em ordem crescente ou decrescente. Ao usar várias colunas de classificação, delimite a lista com vírgulas.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Destinos SQL &#40;página Gerenciador de Conexões&#41;](../../2014/integration-services/sql-destination-editor-connection-manager-page.md)   
 [Editor de Destinos SQL &#40;página Mapeamentos&#41;](../../2014/integration-services/sql-destination-editor-mappings-page.md)   
 [Carregar dados em massa por meio do destino do SQL Server](data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
  
