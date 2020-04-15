---
title: Programa de Administração | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306637"
---
# <a name="administration-program"></a>Programa de administração
> [!NOTE]  
>  Começando com o Windows XP e o Windows Server 2003, o ODBC está incluído no sistema operacional windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 Um programa de administração, o Administrador ODBC, está incluído no SDK do Windows SDK/MDAC. Este programa pode ser redistribuído pelos usuários do SDK. Além disso, os desenvolvedores podem escrever seus próprios programas de administração. Geralmente, os desenvolvedores escrevem seus próprios programas de administração apenas se quiserem manter controle completo sobre a configuração de origem de dados ou se estiverem configurando fontes de dados diretamente de um aplicativo que está agindo como um programa de administração. Por exemplo, um programa de planilha pode permitir que os usuários adicionem e, em seguida, usem fontes de dados em tempo de execução.  
  
 O programa de administração primeiro carrega o instalador DLL. Em seguida, ele chama funções no instalador DLL para executar as seguintes tarefas:  
  
-   **Adicionar, modificar ou excluir fontes de dados de forma interativa.** O programa de administração pode chamar **SQLManageDataSources,** **SQLCreateDataSource**ou **SQLConfigDataSource**.  
  
     **SQLManageDataSources** exibe uma caixa de diálogo com a qual o usuário pode adicionar, modificar ou excluir fontes de dados e especificar opções de rastreamento; esta função é chamada quando o instalador DLL é invocado diretamente do Painel de Controle. **SQLCreateDataSource** exibe uma caixa de diálogo com a qual o usuário só pode adicionar fontes de dados. **SQLConfigDataSource** passa a chamada diretamente para a Configuração do driver DLL.  
  
     Em todos os casos, o instalador DLL chama **ConfigDSN** na configuração do driver DLL para realmente adicionar, modificar ou excluir a fonte de dados. A configuração do driver DLL pode solicitar ao usuário informações adicionais.  
  
-   **Adicione, modifique ou exclua as fontes de dados silenciosamente.** O programa de administração chama **SQLConfigDataSource** no instalador DLL e passa-o como uma alça de janela nula, o nome de uma fonte de dados para adicionar, modificar ou excluir e uma lista de valores para o registro. O instalador DLL chama **ConfigDSN** na configuração do driver DLL para realmente adicionar, modificar ou excluir a fonte de dados.  
  
-   **Adicionar, modificar ou excluir uma fonte de dados padrão.** A fonte de dados padrão é a mesma de qualquer outra fonte de dados, exceto que seu nome é Default. Ele é adicionado, modificado ou excluído da mesma forma que qualquer outra fonte de dados.
