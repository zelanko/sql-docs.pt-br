---
title: Configurações (BD SQL do Azure) do projeto (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 57002374-0d4d-43c1-b4e9-cbec02355a9c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 14fa0cb949505ab2aeb15d1236add9acba9a1ab1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62703724"
---
# <a name="project-settings-azure-sql-db--sybasetosql"></a>Configurações do projeto (BD SQL do Azure) (SybaseToSQL)
As configurações de projeto de BD SQL do Azure permitem que você configurar o sufixo do banco de dados SQL do Azure a serem adicionados na caixa de diálogo de conexão e também permite implementar o mecanismo de pulsação na conexão de BD SQL do Azure.  
  
O painel de BD SQL do Azure está disponível na **configurações do projeto** e **configurações do projeto padrão** caixas de diálogo.  
  
-   Use a caixa de diálogo de configurações do projeto para definir opções de configuração para o projeto atual. Para acessar as configurações de BD SQL do Azure, nos **ferramentas** menu, selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione  **Banco de dados SQL do Azure**.  
  
-   Use a caixa de diálogo de configurações de projeto padrão para definir opções de configuração para todos os projetos. Para acessar as configurações de BD SQL do Azure, nos **ferramentas** menu, selecione **DefaultProject configurações**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **Banco de dados SQL do azure**.  
  
## <a name="connectivity"></a>Conectividade  
**Intervalo de pulsação**  
  
Especifica um intervalo de tempo a ser usado para o mecanismo de pulsação para manter a conexão de BD SQL do Azure ativo no ' minutos: formato de segundos.  
  
**Valor padrão**:' 4:45 '  
  
O valor deve ser especificado em Estou: formato dos ss (por exemplo, ' 4:45 ' ou ' 0:50 ').  
  
**Sufixo do servidor de banco de dados SQL do Azure**  
  
Especifica um sufixo de servidor de BD SQL do Azure  
  
**Valor padrão**: 'database.windows.net'.  
  
