---
title: Configurações de conversão (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f551cf6e-1575-4206-9cca-975b5b43a6b8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7026828bff099b131556dbffd3d990c695bd5ff2
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51662475"
---
# <a name="conversion-settings-mysqltosql"></a>Configurações de conversão (MySQLToSQL)
O **'Configurações'** guia permite que o usuário defina as configurações de nível de nó. Na guia estará disponível nos seguintes nós da Metabase:  
  
-   Nó de banco de dados  
  
-   Categoria de funções  
  
-   Nó de função  
  
-   Categoria de tabelas  
  
-   Nó de tabela  
  
## <a name="specifications"></a>Especificações:  
O **configurações** guia tem duas configurações de usuário, de visualização.:  
  
1.  Conversão de função  
  
2.  Conversão de tabela  
  
Essas configurações estarão disponíveis com base no tipo de nó de Metabase. Por exemplo, conversão de função relacionados ao definir não estarão disponível em um nó da tabela  
  
> [!NOTE]  
> -   As alterações feitas pelo usuário serão salvas no espaço de trabalho do projeto como um arquivo separado de preferência.  
> -   A extensão deste arquivo serão **ccprefs**.  
  
1.  **Configuração da função de conversão:**  
  
    1.  Essa guia conterá **'Forçar a conversão de função'** opção. A opção pode ter um dos quatro valores a seguir:  
  
        -   Converter de acordo com as configurações de projeto [herdadas]  
  
        -   Sempre converter para uma função  
  
        -   Sempre converter em um procedimento  
  
        -   Converter de acordo com as configurações de projeto  
  
    2.  Com base nas configurações, a função será ser convertida para uma função ou um procedimento armazenado.  
  
    3.  As configurações feitas pelo usuário são salvas no arquivo de preferências em cascata, ao clicar em **aplicar** botão.  
  
2.  **Configuração da conversão de tabela:**  
  
    1.  Essa guia conterá **'Geração de coluna auxiliar ROWID Suprimir'** opção. A opção pode ter um dos quatro valores a seguir:  
  
        -   Converter de acordo com as configurações de projeto [herdadas]  
  
        -   Sim  
  
        -   não  
  
        -   Converter de acordo com as configurações de projeto  
  
    2.  Se **'Sim'**, essa configuração impede a criação de criação de coluna auxiliar ROWID em tabelas de destino.  
  
    3.  As configurações feitas pelo usuário são salvas no arquivo de preferências em cascata ao clicar em **aplicar** botão.  
  
## <a name="see-also"></a>Consulte também  
[Configurações do projeto (conversão) (MySQL para o SQL)](https://msdn.microsoft.com/7ad5fe44-6445-4ba8-a457-5af792631f11)  
  
