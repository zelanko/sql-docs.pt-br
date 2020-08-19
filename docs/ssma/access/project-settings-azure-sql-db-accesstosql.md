---
description: Configurações do projeto (banco de dados SQL do Azure) (AccessToSQL)
title: Configurações do projeto (banco de dados SQL do Azure) (AccessToSQL) | Microsoft Docs
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 9954fe012158526e87bd30512b13eca0314bc00e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418542"
---
# <a name="project-settings-azure-sql-database-accesstosql"></a>Configurações do projeto (banco de dados SQL do Azure) (AccessToSQL)
As configurações do projeto SQL Azure permitem que você configure o sufixo do banco de dados SQL do Azure a ser adicionado na caixa de diálogo de conexão e também permita a implementação do mecanismo de pulsação na conexão SQL Azure.  
  
O painel de SQL Azure está disponível nas caixas de diálogo **configurações do projeto** e **configurações do projeto padrão** .  
  
-   Use a caixa de diálogo Configurações do projeto para definir opções de configuração para o projeto atual. Para acessar as configurações de SQL Azure, no menu **ferramentas** , selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **SQL Azure**.  
  
-   Use a caixa de diálogo Configurações de projeto padrão para definir opções de configuração para todos os projetos. Para acessar as configurações de SQL Azure, no menu **ferramentas** , selecione **configurações de defaultproject**, selecione o tipo de projeto como "SQL Azure" na caixa de combinação **versão de destino de migração** para acessar as configurações no painel SQL Azure, clique em **geral** na parte inferior do painel esquerdo e selecione **SQL Azure**.  
  
## <a name="options"></a>Opções  
  
## <a name="connectivity"></a>Conectividade  
**Intervalo de pulsação**  
  
Especifica um intervalo de tempo a ser usado para o mecanismo de pulsação para manter a conexão de SQL Azure ativada no formato ' minutes: segundos '.  
  
**Valor padrão**: ' 4:45 '  
  
O valor deve ser especificado no formato ' m:SS ' (por exemplo, ' 4:45 ' ou ' 0:50 ').  
  
**Sufixo de servidor SQL Azure**  
  
Especifica o sufixo do servidor SQL Azure  
  
**Valor padrão**: ' Database.Windows.net '.  
  
