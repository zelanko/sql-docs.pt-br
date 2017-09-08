---
title: "Configurações (banco de dados do SQL Azure) do projeto (MySQLToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 8c06420a-533b-4de0-948d-a0c6b368c544
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d56834df6e86edcf9821781faa1144afaa2d8d6e
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-azure-sql-db-mysqltosql"></a>Configurações (banco de dados do SQL Azure) do projeto (MySQLToSQL)
As configurações de projeto do SQL Azure permitem que você configure o sufixo do banco de dados do SQL Azure para serem adicionadas na caixa de diálogo de conexão e também permitem implementar o mecanismo de pulsação na conexão do SQL Azure.  
  
O painel do SQL Azure está disponível na **configurações de projeto** e **configurações de projeto padrão** caixas de diálogo.  
  
-   Use a caixa de diálogo de configurações do projeto para definir opções de configuração para o projeto atual. Para acessar as configurações do SQL Azure, no **ferramentas** menu, selecione **configurações de projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **SQL Azure**.  
  
-   Use a caixa de diálogo de configurações de projeto padrão para definir opções de configuração para todos os projetos. Para acessar as configurações do SQL Azure, no **ferramentas** menu, selecione **DefaultProject configurações**, selecione o tipo de projeto de migração como SQL Azure **versão de destino de migração** lista suspensa para acessar as configurações no painel do SQL Azure, clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **SQL Azure**.  
  
## <a name="options"></a>Opções  
  
## <a name="connectivity"></a>Conectividade  
**Intervalo de pulsação**  
  
Especifica um intervalo de tempo a ser usado para o mecanismo de pulsação para manter a conexão do SQL Azure ativa em ' minutos: formato de segundos.  
  
**Valor padrão**:' 4:45 '  
  
O valor deve ser especificado em Estou: formato dos ss (por exemplo, ' 4:45 ' ou ' 0:50 ').  
  
**Sufixo do SQL Server do Azure**  
  
Especifica o sufixo do servidor do SQL Azure  
  
**Valor padrão**: 't'.  
  

