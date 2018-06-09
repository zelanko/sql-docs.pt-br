---
title: Configurações (conversão) (AccessToSQL) do projeto | Microsoft Docs
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
- conversion, options described
- Project Settings dialog box, Conversion
ms.assetid: bcebc635-c638-4ddb-924c-b9ccfef86388
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0d910b3d32f9ff05571fd965d29ac3028cc43144
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34774562"
---
# <a name="project-settings-conversion-accesstosql"></a>Configurações de projeto (conversão) (AccessToSQL)
As configurações de projeto de conversão permitem que você configure como os objetos são convertidos de objetos de banco de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos de banco de dados do SQL Azure.  
  
O painel de conversão está disponível na **configurações de projeto** e **configurações de projeto padrão** caixas de diálogo.  
  
-   Use o **configurações de projeto** caixa de diálogo para definir opções de configuração para o projeto atual. Para acessar as configurações de conversão no **ferramentas** menu, selecione **configurações de projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **conversão**.  
  
-   Use o **configurações de projeto padrão** caixa de diálogo para definir opções de configuração para todos os projetos. Para acessar as configurações de conversão no **ferramentas** menu, selecione **configurações de projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibido e alterado de **versão de destino de migração** lista suspensa, clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **conversão**.  
  
## <a name="options"></a>Opções  
**Adicionar a chave primária**  
Cria uma nova chave primária no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou tabela do SQL Azure se uma tabela não tem chave primária ou índice exclusivo.  
  
-   **Modo padrão**: falso  
  
-   **Modo otimista**: falso  
  
-   **Modo de inteira**: True  
  
Quando conectado ao SQL Azure, é por padrão True. **Adicionar colunas de carimbo de hora**  
Especifica se o SSMA deve criar um valor de carimbo de hora se for necessário.  
  
-   **Modo padrão**: SSMA permitem decidir  
  
-   **Modo otimista**: nunca  
  
-   **Modo de inteira**: SSMA permitem decidir  
  
**Incluir um relatório de avaliação de dados com relatórios de avaliação de conversão**  
Inclui uma avaliação de dados no relatório de avaliação.  
  
-   **Modo padrão**: True  
  
-   **Modo otimista**: falso  
  
-   **Modo de inteira**: True  
  
**Tipo de mensagem quando uma chave primária inclui colunas anuláveis**  
Especifica o tipo de mensagem (aviso, erro ou nada) SSMA mostra no painel de saída ao encontrar chaves primárias com colunas anuláveis.  
  
-   **Modo padrão**: aviso  
  
-   **Modo otimista**: nenhuma mensagem  
  
-   **Modo de inteira**: erro  
  
**Tipo de mensagem quando colunas de chave estrangeira são de tamanhos diferentes**  
Especifica o tipo de mensagem (aviso, erro ou nada) SSMA mostra no painel de saída quando ele encontra uma chave estrangeira de texto incorreta.  
  
-   **Modo padrão**: aviso  
  
-   **Modo otimista**: nenhuma mensagem  
  
-   **Modo de inteira**: erro  
  
**Tipo de mensagem quando colunas de memorando são indexadas**  
Especifica o tipo de mensagem (aviso, erro ou nada) SSMA mostra no painel de saída quando encontrar um índice que contém um **memorando** coluna.  
  
-   **Modo padrão**: aviso  
  
-   **Modo otimista**: nenhuma mensagem  
  
-   **Modo de inteira**: erro  
  
**Avisar quando uma consulta complexa usa um caractere curinga (\&#42;)**  
Exibe um aviso no painel de saída e a lista de erros quando um nome de coluna em uma instrução SELECT é um caractere curinga (*).  
  
-   **Modo padrão**: True  
  
-   **Modo otimista**: falso  
  
-   **Modo de inteira**: True  
  
**Avisar quando o nome do identificador é alterado**  
Exibe uma mensagem no relatório de avaliação e no painel de saída quando um nome de identificador de objeto é alterado por SSMA.  
  
-   **Modo padrão**: True  
  
-   **Modo otimista**: falso  
  
-   **Modo de inteira**: True  
  
**Avisar ao identificador serão ser colocado entre aspas**  
Exibe uma mensagem no relatório de avaliação e no painel de saída quando um nome de identificador de objeto será cotado por SSMA. É necessário delimitar identificadores, quando o nome é uma palavra-chave ou contém caracteres especiais.  
  
-   **Modo padrão**: True  
  
-   **Modo otimista**: falso  
  
-   **Modo de inteira**: True  
  
## <a name="see-also"></a>Consulte também  
[Reference(Access) de Interface do usuário](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
