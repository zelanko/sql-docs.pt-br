---
title: Configurações do projeto (conversão) (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- conversion, options described
- Project Settings dialog box, Conversion
ms.assetid: bcebc635-c638-4ddb-924c-b9ccfef86388
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: ff44d34e6c701c8d43260982d3117def4cb9530d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67929452"
---
# <a name="project-settings-conversion-accesstosql"></a>Configurações do projeto (conversão) (AccessToSQL)
As configurações do projeto de conversão permitem que você configure como os objetos são convertidos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de objetos de banco de dados do Access ou SQL Azure objetos de banco de dados.  
  
O painel de conversão está disponível nas caixas de diálogo **configurações do projeto** e **configurações do projeto padrão** .  
  
-   Use a caixa de diálogo **configurações do projeto** para definir opções de configuração para o projeto atual. Para acessar as configurações de conversão, no menu **ferramentas** , selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **conversão**.  
  
-   Use a caixa de diálogo **configurações de projeto padrão** para definir opções de configuração para todos os projetos. Para acessar as configurações de conversão, no menu **ferramentas** , selecione **configurações de projeto padrão**, selecione tipo de projeto de migração para o qual as configurações devem ser exibidas/Changed do menu suspenso **versão de destino de migração** , clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **conversão**.  
  
## <a name="options"></a>Opções  
**Adicionar chave primária**  
Cria uma nova chave primária na tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure se uma tabela de acesso não tiver nenhuma chave primária ou índice exclusivo.  
  
-   **Modo padrão**: false  
  
-   **Modo otimista**: false  
  
-   **Modo completo**: verdadeiro  
  
Quando conectado a SQL Azure, ele é true padrão. **Adicionar colunas de carimbo de data/hora**  
Especifica se o SSMA deve criar um valor de carimbo de data/hora se for necessário.  
  
-   **Modo padrão**: permitir que o SSMA decida  
  
-   **Modo otimista**: nunca  
  
-   **Modo completo**: permitir que o SSMA decida  
  
**Incluir um relatório de avaliação de dados com relatórios de avaliação de conversão**  
Inclui uma avaliação de dados no relatório de avaliação.  
  
-   **Modo padrão**: verdadeiro  
  
-   **Modo otimista**: false  
  
-   **Modo completo**: verdadeiro  
  
**Tipo de mensagem quando uma chave primária inclui colunas anuláveis**  
Especifica o tipo de mensagem (aviso, erro ou nada) que o SSMA mostra no painel de saída quando encontra chaves primárias com colunas anuláveis.  
  
-   **Modo padrão**: aviso  
  
-   **Modo otimista**: nenhuma mensagem  
  
-   **Modo completo**: erro  
  
**Tipo de mensagem quando as colunas de chave estrangeira são de tamanhos diferentes**  
Especifica o tipo de mensagem (aviso, erro ou nada) que o SSMA mostra no painel de saída quando encontra uma chave estrangeira de texto incorreta.  
  
-   **Modo padrão**: aviso  
  
-   **Modo otimista**: nenhuma mensagem  
  
-   **Modo completo**: erro  
  
**Tipo de mensagem quando as colunas de memorando são indexadas**  
Especifica o tipo de mensagem (aviso, erro ou nada) que o SSMA mostra no painel de saída quando encontra um índice que contém uma coluna de **memorando** .  
  
-   **Modo padrão**: aviso  
  
-   **Modo otimista**: nenhuma mensagem  
  
-   **Modo completo**: erro  
  
**Avisar quando uma consulta complexa usar um curinga (\&#42;)**  
Exibe um aviso no painel de saída e Lista de Erros quando um nome de coluna em uma instrução SELECT é um curinga (*).  
  
-   **Modo padrão**: verdadeiro  
  
-   **Modo otimista**: false  
  
-   **Modo completo**: verdadeiro  
  
**Avisar quando o nome do identificador for alterado**  
Exibe uma mensagem no relatório de avaliação e no painel de saída quando um nome de identificador de objeto é alterado pelo SSMA.  
  
-   **Modo padrão**: verdadeiro  
  
-   **Modo otimista**: false  
  
-   **Modo completo**: verdadeiro  
  
**Avisar quando o identificador estiver entre aspas**  
Exibe uma mensagem no relatório de avaliação e no painel de saída quando um nome de identificador de objeto for citado pelo SSMA. Identificadores de aspas são necessários quando o nome é uma palavra-chave ou contém caracteres especiais.  
  
-   **Modo padrão**: verdadeiro  
  
-   **Modo otimista**: false  
  
-   **Modo completo**: verdadeiro  
  
## <a name="see-also"></a>Consulte Também  
[Referência da interface do usuário (Access)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
