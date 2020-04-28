---
title: Configurações do projeto (banco de BD SQL do Azure) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 57002374-0d4d-43c1-b4e9-cbec02355a9c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 829e7b0c51cd341193944fb2f28241f48618c407
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "70176228"
---
# <a name="project-settings-azure-sql-db--sybasetosql"></a>Configurações do projeto (BD SQL do Azure) (SybaseToSQL)
As configurações do projeto do BD SQL do Azure permitem configurar o sufixo do banco de dados SQL do Azure a ser adicionado na caixa de diálogo de conexão e também permitir a implementação do mecanismo de pulsação na conexão do BD SQL do Azure.  
  
O painel BD SQL do Azure está disponível nas caixas de diálogo **configurações do projeto** e **configurações padrão do projeto** .  
  
-   Use a caixa de diálogo Configurações do projeto para definir opções de configuração para o projeto atual. Para acessar as configurações do BD SQL do Azure, no menu **ferramentas** , selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e selecione **BD SQL do Azure**.  
  
-   Use a caixa de diálogo Configurações de projeto padrão para definir opções de configuração para todos os projetos. Para acessar as configurações do BD SQL do Azure, no menu **ferramentas** , selecione **configurações do defaultproject**, clique em **geral** na parte inferior do painel esquerdo e selecione **BD SQL do Azure**.  
  
## <a name="connectivity"></a>Conectividade  
**Intervalo de pulsação**  
  
Especifica um intervalo de tempo a ser usado para o mecanismo de pulsação para manter a conexão do banco de BD SQL do Azure ativa no formato ' minutos: segundos '.  
  
**Valor padrão**: ' 4:45 '  
  
O valor deve ser especificado no formato ' m:SS ' (por exemplo, ' 4:45 ' ou ' 0:50 ').  
  
**Sufixo do servidor do banco de BD SQL do Azure**  
  
Especifica um sufixo de servidor de banco de BD SQL do Azure  
  
**Valor padrão**: ' Database.Windows.net '.  
  
