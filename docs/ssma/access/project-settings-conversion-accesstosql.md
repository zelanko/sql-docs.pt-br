---
title: Configurações (conversão) (AccessToSQL) do projeto | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 2489442eb8de9d8d0ebfb5d8ed902dd2792e22f2
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51675595"
---
# <a name="project-settings-conversion-accesstosql"></a>Configurações do projeto (conversão) (AccessToSQL)
As configurações de conversão do projeto permitem que você configure como os objetos são convertidos de objetos de banco de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos de banco de dados do SQL Azure.  
  
O painel de conversão está disponível na **configurações do projeto** e **configurações do projeto padrão** caixas de diálogo.  
  
-   Use o **configurações do projeto** caixa de diálogo para definir opções de configuração para o projeto atual. Para acessar as configurações de conversão na **ferramentas** menu, selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione  **Conversão**.  
  
-   Use o **configurações de projeto padrão** caixa de diálogo para definir opções de configuração para todos os projetos. Para acessar as configurações de conversão na **ferramentas** menu, selecione **configurações do projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibida / alterado de  **Versão de destino de migração** lista suspensa, clique em **gerais** na parte inferior do painel esquerdo e, em seguida, selecione **conversão**.  
  
## <a name="options"></a>Opções  
**Adicione a chave primária**  
Cria uma nova chave primária no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou tabela do SQL Azure se uma tabela do Access não tem nenhuma chave primária ou índice exclusivo.  
  
-   **Modo padrão**: False  
  
-   **Modo otimista**: False  
  
-   **Modo de inteira**: True  
  
Quando conectado ao SQL Azure, é por padrão True. **Adicionar colunas de carimbo de hora**  
Especifica se o SSMA deve criar um valor de carimbo de hora, se for necessário.  
  
-   **Modo padrão**: SSMA permitem decidir  
  
-   **Modo otimista**: nunca  
  
-   **Modo de inteira**: SSMA permitem decidir  
  
**Incluir um relatório de avaliação de dados com relatórios de avaliação de conversão**  
Inclui uma avaliação de dados no relatório de avaliação.  
  
-   **Modo padrão**: True  
  
-   **Modo otimista**: False  
  
-   **Modo de inteira**: True  
  
**Tipo de mensagem quando uma chave primária inclui colunas que permitem valor nulas**  
Especifica o tipo de mensagem (aviso, erro ou nada) SSMA mostra no painel de saída quando ele encontra chaves primárias com colunas que permitem valor nulas.  
  
-   **Modo padrão**: aviso  
  
-   **Modo otimista**: nenhuma mensagem  
  
-   **Modo de inteira**: erro  
  
**Tipo de mensagem quando as colunas de chave estrangeira são de tamanhos diferentes**  
Especifica o tipo de mensagem (aviso, erro ou nada) SSMA mostra no painel de saída quando ele encontra uma chave estrangeira de texto incorreta.  
  
-   **Modo padrão**: aviso  
  
-   **Modo otimista**: nenhuma mensagem  
  
-   **Modo de inteira**: erro  
  
**Tipo de mensagem quando as colunas de memorando são indexadas**  
Especifica o tipo de mensagem (aviso, erro ou nada) SSMA mostra no painel de saída quando ele encontra um índice que contém um **memorando** coluna.  
  
-   **Modo padrão**: aviso  
  
-   **Modo otimista**: nenhuma mensagem  
  
-   **Modo de inteira**: erro  
  
**Avisar quando uma consulta complexa usa um caractere curinga (\&#42;)**  
Exibe um aviso no painel de saída e lista de erros quando um nome de coluna em uma instrução SELECT é um caractere curinga (*).  
  
-   **Modo padrão**: True  
  
-   **Modo otimista**: False  
  
-   **Modo de inteira**: True  
  
**Avisar quando o nome do identificador é alterado**  
Exibe uma mensagem no relatório de avaliação e no painel de saída quando um nome de identificador de objeto é alterado pelo SSMA.  
  
-   **Modo padrão**: True  
  
-   **Modo otimista**: False  
  
-   **Modo de inteira**: True  
  
**Avisar quando o identificador será ser colocado entre aspas**  
Exibe uma mensagem no relatório de avaliação e no painel de saída quando um nome de identificador de objeto será cotado por SSMA. Delimitar identificadores é necessário quando o nome é uma palavra-chave ou contém caracteres especiais.  
  
-   **Modo padrão**: True  
  
-   **Modo otimista**: False  
  
-   **Modo de inteira**: True  
  
## <a name="see-also"></a>Consulte também  
[Reference(Access) de Interface do usuário](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
