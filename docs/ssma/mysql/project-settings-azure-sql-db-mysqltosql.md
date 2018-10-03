---
title: Configurações (BD SQL do Azure) do projeto (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8c06420a-533b-4de0-948d-a0c6b368c544
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b319db9bb867e94e2a7400acffe9fb87ccb6b7b8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47756196"
---
# <a name="project-settings-azure-sql-db-mysqltosql"></a>Configurações do projeto (BD SQL do Azure) (MySQLToSQL)
As configurações do projeto do SQL Azure permitem que você configurar o sufixo do banco de dados do SQL Azure a serem adicionados na caixa de diálogo de conexão e também permite implementar o mecanismo de pulsação na conexão do SQL Azure.  
  
O painel do SQL Azure está disponível na **configurações do projeto** e **configurações do projeto padrão** caixas de diálogo.  
  
-   Use a caixa de diálogo de configurações do projeto para definir opções de configuração para o projeto atual. Para acessar as configurações do SQL Azure, nos **ferramentas** menu, selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **SQL Azure**.  
  
-   Use a caixa de diálogo de configurações de projeto padrão para definir opções de configuração para todos os projetos. Para acessar as configurações do SQL Azure, no **ferramentas** menu, selecione **DefaultProject configurações**, selecione o tipo de projeto de migração como SQL Azure da **versão de destino de migração** drop para baixo até o acesso as configurações no painel do SQL Azure, clique em **gerais** na parte inferior do painel esquerdo e, em seguida, selecione **SQL Azure**.  
  
## <a name="options"></a>Opções  
  
## <a name="connectivity"></a>Conectividade  
**Intervalo de pulsação**  
  
Especifica um intervalo de tempo a ser usado para o mecanismo de pulsação para manter a conexão do SQL Azure ativo no ' minutos: formato de segundos.  
  
**Valor padrão**:' 4:45 '  
  
O valor deve ser especificado em Estou: formato dos ss (por exemplo, ' 4:45 ' ou ' 0:50 ').  
  
**Sufixo de servidor do SQL Azure**  
  
Especifica o sufixo do servidor do SQL Azure  
  
**Valor padrão**: 'database.windows.net'.  
  
