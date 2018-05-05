---
title: Configurações (banco de dados do SQL Azure) do projeto (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 57002374-0d4d-43c1-b4e9-cbec02355a9c
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 41c429bd09254580e705131988882402e227761c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="project-settings-azure-sql-db--sybasetosql"></a>Configurações (banco de dados do SQL Azure) do projeto (SybaseToSQL)
As configurações de projeto de banco de dados de SQL do Azure permitem que você configure o sufixo de banco de dados de banco de dados do Azure SQL para ser adicionado na caixa de diálogo de conexão e também permitem implementar o mecanismo de pulsação na conexão de banco de dados de SQL do Azure.  
  
O painel de banco de dados de SQL Azure está disponível na **configurações de projeto** e **configurações de projeto padrão** caixas de diálogo.  
  
-   Use a caixa de diálogo de configurações do projeto para definir opções de configuração para o projeto atual. Para acessar as configurações de banco de dados de SQL do Azure, no **ferramentas** menu, selecione **configurações de projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **Azure SQL DB**.  
  
-   Use a caixa de diálogo de configurações de projeto padrão para definir opções de configuração para todos os projetos. Para acessar as configurações de banco de dados de SQL do Azure, no **ferramentas** menu, selecione **DefaultProject configurações**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **Azure SQL DB**.  
  
## <a name="connectivity"></a>Conectividade  
**Intervalo de pulsação**  
  
Especifica um intervalo de tempo a ser usado para o mecanismo de pulsação para manter a conexão de banco de dados do Azure SQL ativa em ' minutos: formato de segundos.  
  
**Valor padrão**:' 4:45 '  
  
O valor deve ser especificado em Estou: formato dos ss (por exemplo, ' 4:45 ' ou ' 0:50 ').  
  
**Sufixo de servidor de banco de dados SQL do Azure**  
  
Especifica um sufixo de servidor de banco de dados de SQL do Azure  
  
**Valor padrão**: 't'.  
  
