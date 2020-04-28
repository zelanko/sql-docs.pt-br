---
title: Programa de administração | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- administration program [ODBC]
- ODBC administrator [ODBC]
ms.assetid: a6c8248a-7a01-42e7-aaed-99dc94d50028
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d8a2a8363371d6f6c3644c2b7b49aa77644d496e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306637"
---
# <a name="administration-program"></a>Programa de administração
> [!NOTE]  
>  A partir do Windows XP e do Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 Um programa de administração, o Administrador ODBC, está incluído no SDK do SDK do Windows/MDAC. Este programa e pode ser redistribuído por usuários do SDK. Além disso, os desenvolvedores podem escrever seus próprios programas de administração. Em geral, os desenvolvedores escrevem seus próprios programas de administração apenas se desejarem manter o controle completo sobre a configuração da fonte de dados ou se estiverem Configurando fontes de dados diretamente de um aplicativo que esteja agindo como um programa de administração. Por exemplo, um programa de planilha pode permitir que os usuários adicionem e, em seguida, usem fontes de dados em tempo de execução.  
  
 O programa de administração primeiro carrega a DLL do instalador. Em seguida, ele chama funções na DLL do instalador para executar as seguintes tarefas:  
  
-   **Adicionar, modificar ou excluir fontes de dados interativamente.** O programa de administração pode chamar **SQLManageDataSources**, **SQLCreateDataSource**ou **SQLConfigDataSource**.  
  
     **SQLManageDataSources** exibe uma caixa de diálogo com a qual o usuário pode adicionar, modificar ou excluir fontes de dados e especificar opções de rastreamento; Essa função é chamada quando a DLL do instalador é invocada diretamente do painel de controle. **SQLCreateDataSource** exibe uma caixa de diálogo com a qual o usuário só pode adicionar fontes de dados. **SQLConfigDataSource** passa a chamada diretamente para a DLL de instalação do driver.  
  
     Em todos os casos, a DLL do instalador chama **ConfigDSN** na DLL de instalação do driver para, na verdade, adicionar, modificar ou excluir a fonte de dados. A DLL de instalação do driver pode solicitar informações adicionais ao usuário.  
  
-   **Adicionar, modificar ou excluir fontes de dados silenciosamente.** O programa de administração chama **SQLConfigDataSource** na DLL do instalador e passa a ele um identificador de janela nulo, o nome de uma fonte de dados para adicionar, modificar ou excluir e uma lista de valores para o registro. A DLL do instalador chama **ConfigDSN** na DLL de instalação do driver para, na verdade, adicionar, modificar ou excluir a fonte de dados.  
  
-   **Adicionar, modificar ou excluir uma fonte de dados padrão.** A fonte de dados padrão é igual a qualquer outra fonte de dados, exceto que seu nome é padrão. Ela é adicionada, modificada ou excluída da mesma maneira que qualquer outra fonte de dados.
