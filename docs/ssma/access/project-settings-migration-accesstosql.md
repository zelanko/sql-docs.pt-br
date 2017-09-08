---
title: "Configurações (migração) (AccessToSQL) do projeto | Microsoft Docs"
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
helpviewer_keywords:
- Migration settings
- Project Settings dialog box, Migration
ms.assetid: 4caebc9c-8680-4b99-a8fa-89c43161c95d
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3faaf19a1c591628ef97c4fe33fa0a54d4b077d5
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-migration-accesstosql"></a>Configurações de projeto (migração) (AccessToSQL)
As configurações de projeto de migração lhe permitem configurar como os dados são migrados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.  
  
O painel de migração está disponível na **configurações de projeto** e **configurações de projeto padrão** caixas de diálogo.  
  
-   Use o **configurações de projeto** caixa de diálogo para definir opções de configuração para o projeto atual. Para acessar as configurações de migração no **ferramentas** menu, selecione **configurações de projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique **migração**.  
  
-   Use o **configurações de projeto padrão** caixa de diálogo para definir opções de configuração para todos os projetos. Para acessar as configurações de migração no **ferramentas** menu, selecione **configurações de projeto padrão**, selecione o tipo de projeto em **versão de destino de migração** caixa de combinação do qual você deseja acessar as configurações, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique **migração**.  
  
## <a name="options"></a>Opções  
**Verificar restrições**  
Especifica se o SSMA deve verificar restrições ao adicionar dados às tabelas.  
  
-   **Modo padrão**: falso  
  
-   **Modo otimista**: True  
  
-   **Modo de inteira**: falso  
  
**Acionadores**  
Especifica se o SSMA deve ativar gatilhos de inserção quando ele adiciona dados a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tabelas.  
  
-   **Modo padrão**: falso  
  
-   **Modo otimista**: True  
  
-   **Modo de inteira**: falso  
  
**Manter identidade**  
Especifica se o SSMA preserva valores de identidade de acesso quando ele adiciona dados a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Se esse valor for False, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] atribui valores de identidade.  
  
-   **Modo padrão**: True  
  
-   **Modo otimista**: True  
  
-   **Modo de inteira**: falso  
  
**Manter nulos**  
Especifica se o SSMA preserva valores nulos na fonte de dados quando ele adiciona dados a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], independentemente dos valores padrão que são especificados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   **Modo padrão**: True  
  
-   **Modo otimista**: falso  
  
-   **Modo de inteira**: True  
  
**Bloqueios de tabela**  
Especifica se o SSMA bloqueia tabelas ao adicionar dados às tabelas durante a migração de dados. Se o valor for False, o SSMA usa bloqueios de linha.  
  
-   **Modo padrão**: True  
  
-   **Modo otimista**: True  
  
-   **Modo de inteira**: True  
  
**Substitua as datas sem suporte**  
Especifica se o SSMA deve corrigir as datas de acesso mais antigas que o próximo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] datetime data (01 de janeiro de 1753).  
  
-   Para manter os valores de data atual, selecione **não fazer nada**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]datas anteriores a 01 de janeiro de 1753 não aceita em uma coluna de data e hora. Se você usar datas mais antigas, você deve converter os valores de data e hora para valores de caractere.  
  
-   Para converter datas anteriores a 01 de janeiro de 1753 como NULL, selecione **substituir com NULL**.  
  
-   Para substituir as datas anteriores a 01 de janeiro de 1753 com uma data com suporte, selecione **substitua mais próximo da data com suporte**. Se você selecionar esse valor, por padrão mais próximo com suporte de data será selecionada como 01 de janeiro de 1753.  
  
**Tamanho do lote**  
Tamanho do lote usado durante a migração de dados. Uma transação é registrada após cada lote. Por padrão, o tamanho do lote para todos os esquemas é 10000.  
  
## <a name="see-also"></a>Consulte também  
[Reference(Access) de Interface do usuário](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  

