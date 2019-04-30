---
title: Configurações (BD SQL do Azure) do projeto (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Project Settings dialog box, SQL Azure
- SQL Azure settings
ms.assetid: bbb8a204-d0e4-4f0b-9709-271feb1f136e
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2307a62c05503a231c3ee16b79efb25e964f55bd
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63453472"
---
# <a name="project-settings-azure-sql-db-accesstosql"></a>Configurações (BD SQL do Azure) do projeto (AccessToSQL)
As configurações do projeto do SQL Azure permitem que você configurar o sufixo do banco de dados do SQL Azure a serem adicionados na caixa de diálogo de conexão e também permite implementar o mecanismo de pulsação na conexão do SQL Azure.  
  
O painel do SQL Azure está disponível na **configurações do projeto** e **configurações do projeto padrão** caixas de diálogo.  
  
-   Use a caixa de diálogo de configurações do projeto para definir opções de configuração para o projeto atual. Para acessar as configurações do SQL Azure, nos **ferramentas** menu, selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **SQL Azure**.  
  
-   Use a caixa de diálogo de configurações de projeto padrão para definir opções de configuração para todos os projetos. Para acessar as configurações do SQL Azure, nos **ferramentas** menu, selecione **DefaultProject configurações**, selecione o tipo de projeto como "SQL Azure" na **versão de destino de migração** caixa de combinação para acessar as configurações no painel do SQL Azure, clique em **gerais** na parte inferior do painel esquerdo e, em seguida, selecione **SQL Azure**.  
  
## <a name="options"></a>Opções  
  
## <a name="connectivity"></a>Conectividade  
**Intervalo de pulsação**  
  
Especifica um intervalo de tempo a ser usado para o mecanismo de pulsação para manter a conexão do SQL Azure ativo no ' minutos: formato de segundos.  
  
**Valor padrão**:' 4:45 '  
  
O valor deve ser especificado em Estou: formato dos ss (por exemplo, ' 4:45 ' ou ' 0:50 ').  
  
**Sufixo de servidor do SQL Azure**  
  
Especifica o sufixo do servidor do SQL Azure  
  
**Valor padrão**: 'database.windows.net'.  
  
