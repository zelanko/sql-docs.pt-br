---
description: Configurações de conversão (MySQLToSQL)
title: Configurações de conversão (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f551cf6e-1575-4206-9cca-975b5b43a6b8
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 7547984e97bb47a640c162743fe0b069b38f7dff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418462"
---
# <a name="conversion-settings-mysqltosql"></a>Configurações de conversão (MySQLToSQL)
A guia **' configurações '** permite que o usuário defina as configurações de nível de nó. A guia estará disponível nos seguintes nós de metabase:  
  
-   Nó do banco de dados  
  
-   Categoria de funções  
  
-   Nó de função  
  
-   Categoria de tabelas  
  
-   Nó de tabela  
  
## <a name="specifications"></a>As  
A guia **configurações** tem duas configurações de usuário, aula sobre visualização.:  
  
1.  Conversão de função  
  
2.  Conversão de tabela  
  
Essas configurações estarão disponíveis com base no tipo de nó da metabase. Por exemplo, a configuração relacionada à conversão de função não estará disponível no nó de tabela  
  
> [!NOTE]  
> -   As alterações feitas pelo usuário serão salvas no espaço de trabalho do projeto como um arquivo de preferência separado.  
> -   A extensão desse arquivo será **ccprefs**.  
  
1.  **Configuração de conversão de função:**  
  
    1.  Esta guia contém a opção **"forçar conversão de função"** . A opção pode ter um dos quatro valores a seguir:  
  
        -   Converter de acordo com as configurações do projeto [herdado]  
  
        -   Sempre converter em uma função  
  
        -   Sempre converter em um procedimento  
  
        -   Converter de acordo com as configurações do projeto  
  
    2.  Com base nas configurações, a função será convertida em uma função ou em um procedimento armazenado.  
  
    3.  As configurações feitas pelo usuário são salvas no arquivo de preferências em cascata ao clicar no botão **aplicar** .  
  
2.  **Configuração de conversão de tabela:**  
  
    1.  Esta guia contém a opção **' suprimir a geração de colunas auxiliares de ROWID '** . A opção pode ter um dos quatro valores a seguir:  
  
        -   Converter de acordo com as configurações do projeto [herdado]  
  
        -   Sim  
  
        -   Não  
  
        -   Converter de acordo com as configurações do projeto  
  
    2.  Se **' Sim '**, essa configuração proíbe a criação de criação de coluna auxiliar de ROWID em tabelas de destino.  
  
    3.  As configurações feitas pelo usuário são salvas no arquivo de preferências em cascata ao clicar no botão **aplicar** .  
  
## <a name="see-also"></a>Consulte Também  
[Configurações do projeto (conversão) (MySQL para SQL)](https://msdn.microsoft.com/7ad5fe44-6445-4ba8-a457-5af792631f11)  
  
