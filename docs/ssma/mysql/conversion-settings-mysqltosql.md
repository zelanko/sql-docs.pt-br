---
title: "Configurações de conversão (MySQLToSQL) | Microsoft Docs"
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
ms.assetid: f551cf6e-1575-4206-9cca-975b5b43a6b8
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b83e86ce201343d624974244a9d551fb1016d3e7
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="conversion-settings-mysqltosql"></a>Configurações de conversão (MySQLToSQL)
O **'Configurações'** guia permite que o usuário defina as configurações de nível de nó. Na guia estará disponível nos seguintes nós da Metabase:  
  
-   Nó de banco de dados  
  
-   Categoria de funções  
  
-   Nó de função  
  
-   Categoria de tabelas  
  
-   Nó de tabela  
  
## <a name="specifications"></a>Especificações de:  
O **configurações** guia tem duas configurações de usuário, viz.:  
  
1.  Conversão de função  
  
2.  Conversão de tabela  
  
Essas configurações estarão disponíveis com base no tipo de nó de Metabase. Por exemplo, conversão de função relacionados ao definir não estará disponível no nó de tabela  
  
> [!NOTE]  
> -   As alterações feitas pelo usuário serão salvas no espaço de trabalho do projeto como um arquivo separado de preferência.  
> -   A extensão deste arquivo será **ccprefs**.  
  
1.  **Configuração da função de conversão:**  
  
    1.  Essa guia contém **'Forçar a conversão de função'** opção. A opção pode ter um dos quatro valores a seguir:  
  
        -   Converter de acordo com as configurações de projeto [herdadas]  
  
        -   Sempre converter para uma função  
  
        -   Sempre converter em um procedimento  
  
        -   Converter de acordo com as configurações de projeto  
  
    2.  Com base nas configurações, a função será ser convertida para uma função ou um procedimento armazenado.  
  
    3.  As configurações feitas pelo usuário são salvas no arquivo de preferências em cascata quando você clicar em **aplicar** botão.  
  
2.  **Configuração da conversão de tabela:**  
  
    1.  Essa guia contém **'Geração de coluna auxiliar ROWID Suprimir'** opção. A opção pode ter um dos quatro valores a seguir:  
  
        -   Converter de acordo com as configurações de projeto [herdadas]  
  
        -   Sim  
  
        -   Não  
  
        -   Converter de acordo com as configurações de projeto  
  
    2.  Se **'Sim'**, essa configuração impede a criação de criação de coluna auxiliar ROWID nas tabelas de destino.  
  
    3.  As configurações feitas pelo usuário são salvas no arquivo de preferências em cascata quando você clicar em **aplicar** botão.  
  
## <a name="see-also"></a>Consulte também  
[Configurações de projeto (conversão) (MySQL para o SQL)](http://msdn.microsoft.com/en-us/7ad5fe44-6445-4ba8-a457-5af792631f11)  
  

