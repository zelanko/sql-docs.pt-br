---
title: Identificar bancos de dados e tabelas para o Stretch Database | Microsoft Docs
ms.custom: 
ms.date: 10/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: stretch-database
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, identifying databases
- Stretch Database, identifying tables
- identifying databases for Stretch Database
- identifying tables for Stretch Database
ms.assetid: 81bd93d8-eef8-4572-88d7-5c37ab5ac2bf
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c5b4c49b5b2e1c098503bab4e61c8bad0d75f891
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="identify-databases-and-tables-for-stretch-database-with-data-migration-assistant"></a>Identificar bancos de dados e tabelas do Stretch Database com o Assistente de Migração de Dados
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Para identificar bancos de dados e tabelas que são candidatos ao Stretch Database, juntamente com os possíveis problemas de bloqueio, baixe e execute o Assistente de Migração de Dados da Microsoft.
  
## <a name="get-data-migration-assistant"></a>Obter o Assistente de Migração de Dados
 Baixe e instale o Assistente de migração de dados [aqui](https://www.microsoft.com/download/details.aspx?id=53595). Essa ferramenta não está incluída na mídia de instalação do SQL Server.  
  
## <a name="run-data-migration-assistant"></a>Executar o Assistente de Migração de Dados  
  
1.  Execute o Assistente de Migração de Dados da Microsoft.  

2.  Crie um novo projeto do tipo **Avaliação** e dê um nome a ele.

3.  Selecione **SQL Server** como **Tipo de servidor de origem** e **tipo de servidor de destino**.

4.  Selecione **Criar**. 

5. Na página **Opções** (etapa 1), selecione **Recomendação de novos recursos**. Opcionalmente, desmarque a seleção de **Problemas de compatibilidade**.

6.  Na página **Selecionar fontes** (etapa 2), conecte-se a um servidor, selecione um banco de dados e, em seguida, selecione **Adicionar**.

7.  Selecione **Iniciar Avaliação**.

## <a name="review-the-results"></a>Analisar os resultados  
  
1.  Quando a análise for concluída, na página **Examinar resultados** (etapa 3), selecione a opção **Recomendações de recurso** e, em seguida, selecione a guia **Armazenamento**.

2.  Examine as recomendações relacionadas ao Stretch Database. Cada recomendação lista as tabelas para as quais o Stretch Database pode ser apropriado, juntamente com os possíveis problemas de bloqueio.

## <a name="historical-note"></a>Observação histórica
O Assistente do Stretch Database era um componente do Supervisor de Atualização do SQL Server 2016. Nessa época, você precisava selecionar e executar o Assistente do Stretch Database como uma ação separada.

Com o lançamento do Assistente de Migração do Dados, que substitui e estende o Supervisor de Atualização, a funcionalidade do Assistente do Stretch Database é incorporada nessa nova ferramenta. Você não precisa selecionar as opções para obter recomendações relacionadas ao Stretch Database. Ao executar uma Avaliação no Assistente de Migração de Dados, os resultados relacionados ao Stretch Database são exibidos na guia **Armazenamento** das **Recomendações de recurso**.
  
## <a name="next-step"></a>Próxima etapa  
 Habilite o Stretch Database.  
  
-   Para habilitar o Stretch Database em um **banco de dados**, veja [Habilitar o Stretch Database em um banco de dados](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
-   Para habilitar o Stretch Database em outra **tabela**, quando o Stretch já estiver habilitado no banco de dados, veja [Habilitar o Stretch Database para uma tabela](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md). 
  
## <a name="see-also"></a>Consulte Também  
 [Limitações do Stretch Database](../../sql-server/stretch-database/limitations-for-stretch-database.md)   
 [Habilitar o Stretch Database em um banco de dados](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Habilitar o Stretch Database para uma tabela](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
