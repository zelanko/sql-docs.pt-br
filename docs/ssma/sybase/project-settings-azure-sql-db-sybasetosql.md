---
title: Configurações do projeto (banco de dados SQL do Azure) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 57002374-0d4d-43c1-b4e9-cbec02355a9c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: b79d4e94126676e128d803176463b314348ed8a1
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87930917"
---
# <a name="project-settings-azure-sql-database--sybasetosql"></a>Configurações do projeto (banco de dados SQL do Azure) (SybaseToSQL)
As configurações do projeto do banco de dados SQL do Azure permitem configurar o sufixo do banco de dados SQL do Azure a ser adicionado na caixa de diálogo de conexão e também permitir a implementação do mecanismo de pulsação na conexão do banco de dados SQL  
  
O painel banco de dados SQL do Azure está disponível nas caixas de diálogo **configurações do projeto** e **configurações do projeto padrão** .  
  
-   Use a caixa de diálogo Configurações do projeto para definir opções de configuração para o projeto atual. Para acessar as configurações do banco de dados SQL do Azure, no menu **ferramentas** , selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e selecione **banco de dados SQL do Azure**.  
  
-   Use a caixa de diálogo Configurações de projeto padrão para definir opções de configuração para todos os projetos. Para acessar as configurações do banco de dados SQL do Azure, no menu **ferramentas** , selecione **configurações do defaultproject**, clique em **geral** na parte inferior do painel esquerdo e selecione **banco de dados SQL do Azure**.  
  
## <a name="connectivity"></a>Conectividade  
**Intervalo de pulsação**  
  
Especifica um intervalo de tempo a ser usado para o mecanismo de pulsação para manter a conexão do banco de dados SQL do Azure ativa no formato ' minutos: segundos '.  
  
**Valor padrão**: ' 4:45 '  
  
O valor deve ser especificado no formato ' m:SS ' (por exemplo, ' 4:45 ' ou ' 0:50 ').  
  
**Sufixo do servidor do banco de dados SQL do Azure**  
  
Especifica um sufixo de servidor do banco de dados SQL do Azure  
  
**Valor padrão**: ' Database.Windows.net '.  
  
