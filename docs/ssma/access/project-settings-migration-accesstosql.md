---
title: Configurações (migração) (AccessToSQL) do projeto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Migration settings
- Project Settings dialog box, Migration
ms.assetid: 4caebc9c-8680-4b99-a8fa-89c43161c95d
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 10346770784c94fe18357b5717e60f7e3f88a8c7
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "40392233"
---
# <a name="project-settings-migration-accesstosql"></a>Configurações do projeto (migração) (AccessToSQL)
As configurações de projeto de migração permitem que você configure como os dados são migrados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.  
  
O painel de migração está disponível na **configurações do projeto** e **configurações do projeto padrão** caixas de diálogo.  
  
-   Use o **configurações do projeto** caixa de diálogo para definir opções de configuração para o projeto atual. Para acessar as configurações de migração na **ferramentas** menu, selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique  **Migração**.  
  
-   Use o **configurações de projeto padrão** caixa de diálogo para definir opções de configuração para todos os projetos. Para acessar as configurações de migração na **ferramentas** menu, selecione **configurações do projeto padrão**, selecione o tipo de projeto no **versão de destino de migração** caixa de combinação de que você para acessar as configurações, clique em **gerais** na parte inferior do painel esquerdo e, em seguida, clique **migração**.  
  
## <a name="options"></a>Opções  
**Verificar restrições**  
Especifica se o SSMA deve verificar restrições quando ele adiciona dados às tabelas.  
  
-   **Modo padrão**: False  
  
-   **Modo otimista**: True  
  
-   **Modo de inteira**: False  
  
**Acionadores**  
Especifica se o SSMA deve ativar gatilhos de inserção quando ele adiciona dados a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas.  
  
-   **Modo padrão**: False  
  
-   **Modo otimista**: True  
  
-   **Modo de inteira**: False  
  
**Manter identidade**  
Especifica se o SSMA preserva os valores de identidade de acesso quando ele adiciona dados a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se esse valor for False, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribui valores de identidade.  
  
-   **Modo padrão**: True  
  
-   **Modo otimista**: True  
  
-   **Modo de inteira**: False  
  
**Manter nulos**  
Especifica se o SSMA preserva valores nulos na fonte de dados quando ele adiciona dados a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], independentemente dos valores padrão que são especificados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Modo padrão**: True  
  
-   **Modo otimista**: False  
  
-   **Modo de inteira**: True  
  
**Bloqueios de tabela**  
Especifica se o SSMA bloqueia tabelas quando ele adiciona dados às tabelas durante a migração de dados. Se o valor for False, o SSMA usa bloqueios de linha.  
  
-   **Modo padrão**: True  
  
-   **Modo otimista**: True  
  
-   **Modo de inteira**: True  
  
**Substituir datas sem suporte**  
Especifica se o SSMA deve corrigir as datas de acesso anteriores ao mais antigo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] data e hora data (01 de janeiro de 1753).  
  
-   Para manter os valores de data atual, selecione **não fazem nada**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não aceita datas antes de 01 de janeiro de 1753 em uma coluna de data e hora. Se você usar datas mais antigas, você deve converter os valores de data e hora para valores de caractere.  
  
-   Para converter datas antes de 01 de janeiro de 1753 como NULL, selecione **substitua NULL**.  
  
-   Para substituir datas antes de 01 de janeiro de 1753 com uma data com suporte, selecione **substitua mais próximo da data com suporte**. Se você selecionar esse valor, por padrão mais próximo com suporte de data será selecionada como 01 de janeiro de 1753.  
  
**Tamanho do lote**  
Tamanho do lote usado durante a migração de dados. Uma transação é registrada após cada lote. Por padrão, o tamanho do lote para todos os esquemas é 10000.  
  
## <a name="see-also"></a>Consulte também  
[Reference(Access) de Interface do usuário](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
