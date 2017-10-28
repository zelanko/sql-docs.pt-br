---
title: "Bancos de dados e tabelas do Stretch Database – Assistente do Stretch Database | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: 59608301d353d99eb710a956389fd9f8d8948dfe
ms.contentlocale: pt-br
ms.lasthandoff: 07/29/2017

---
# <a name="stretch-database-databases-and-tables---stretch-database-advisor"></a>Bancos de dados e tabelas do Stretch Database – Assistente do Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Para identificar bancos de dados e tabelas que são candidatos ao Stretch Database, baixe o Supervisor de atualização do SQL Server 2016 e execute o Supervisor do Stretch Database. O Supervisor do Stretch Database também identifica problemas de bloqueio.  
  
## <a name="download-and-install-upgrade-advisor"></a>Baixar e instalar o Supervisor de Atualização  
 Baixe e instale o Supervisor de Atualização [aqui](https://www.microsoft.com/en-us/download/details.aspx?id=53595). Essa ferramenta não está incluída na mídia de instalação do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] .  
  
## <a name="run-the-stretch-database-advisor"></a>Executar o Supervisor do Stretch Database  
  
1.  Execute o Supervisor de Atualização.  
  
2.  Selecione **Cenários**e **RUN STRETCH DATABASE ADVISOR**.  
  
3.  Na folha **Executar o Supervisor do Stretch Database** , clique em **SELECT DATABASES TO ANALYZE**.  
  
4.  Na folha **Selecionar bancos de dados** , insira ou selecione o nome do servidor e as informações de autenticação. Clique em **Conectar**.

5.  É exibida uma lista de bancos de dados no servidor selecionado. Selecione os bancos de dados que você deseja analisar. Clique em **Selecionar**.  
  
6.  Na folha **Executar o Supervisor do Stretch Database** , clique em **Executar**.  A análise é executada.  
  
## <a name="review-the-results"></a>Analisar os resultados  
  
1.  Quando a análise for concluída, na folha **Supervisor do Stretch Database** , selecione um dos bancos de dados analisados para exibir a folha **Resultados da análise** .  
  
     A folha **Resultados da Análise** lista as tabelas recomendadas no banco de dados selecionado que correspondem aos critérios de recomendação padrão. 
  
2.  Na lista de tabelas recomendadas, na folha **Resultados da análise** , selecione uma das tabelas recomendadas para exibir a folha **Resultados da tabela** .  
  
     Se houver problemas de bloqueio, a folha **Resultados da Tabela** lista os problemas de bloqueio da tabela selecionada. Para obter informações sobre os problemas de bloqueio detectados pelo Supervisor do Stretch Database, veja [Limitações do Stretch Database](../../sql-server/stretch-database/limitations-for-stretch-database.md).  
  
3.  Na lista de problemas de bloqueio da folha **Resultados da tabela** , selecione um dos problemas para exibir mais informações sobre o problema selecionado e propor etapas de mitigação. Implemente as etapas de mitigação sugeridas se você quiser configurar a tabela selecionada para o Stretch Database.  
  
## <a name="next-step"></a>Próxima etapa  
 Habilite o Stretch Database.  
  
-   Para habilitar o Stretch Database em um **banco de dados**, veja [Habilitar o Stretch Database em um banco de dados](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
-   Para habilitar o Stretch Database em outra **tabela**, quando o Stretch já estiver habilitado no banco de dados, veja [Habilitar o Stretch Database para uma tabela](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md). 
  
## <a name="see-also"></a>Consulte também  
 [Limitações do Stretch Database](../../sql-server/stretch-database/limitations-for-stretch-database.md)   
 [Habilitar o Stretch Database em um banco de dados](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Habilitar o Stretch Database para uma tabela](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  

