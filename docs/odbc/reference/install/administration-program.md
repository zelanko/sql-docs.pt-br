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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 740a09d9a6bceb9d3f290faa71444df0d1e7c6c7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792314"
---
# <a name="administration-program"></a>Programa de administração
> [!NOTE]  
>  Começando com o Windows XP e Windows Server 2003, ODBC está incluído no sistema operacional Windows. Você deve instalar apenas explicitamente ODBC em versões anteriores do Windows.  
  
 Um programa de administração, o administrador de ODBC é incluído com o SDK do MDAC/SDK do Windows. Esse programa e pode ser redistribuído por usuários do SDK. Além disso, os desenvolvedores podem escrever seus próprios programas de administração. Em geral, os desenvolvedores escrevem seus próprios programas de administração somente se eles desejam manter o controle completo sobre a configuração de fonte de dados, ou se estiver configurando a fontes de dados diretamente de um aplicativo que está atuando como um programa de administração. Por exemplo, um programa de planilha pode permitir aos usuários adicionar e, em seguida, usar fontes de dados em tempo de execução.  
  
 O programa de administração pela primeira vez carrega a DLL do instalador. Depois, ele chama funções no instalador do DLL para executar as seguintes tarefas:  
  
-   **Adicionar, modificar ou excluir fontes de dados interativamente.** O programa de administração pode chamar **SQLManageDataSources**, **SQLCreateDataSource**, ou **SQLConfigDataSource**.  
  
     **SQLManageDataSources** exibe uma caixa de diálogo com a qual o usuário pode adicionar, modificar, ou excluir fontes de dados e especifique as opções de rastreamento; essa função é chamada quando a DLL do instalador é invocado diretamente do painel de controle. **SQLCreateDataSource** exibe uma caixa de diálogo com a qual o usuário só pode adicionar fontes de dados. **SQLConfigDataSource** passará a chamada diretamente para a DLL de instalação do driver.  
  
     Em todos os casos, chama a DLL do instalador **ConfigDSN** na configuração do driver DLL, na verdade, adicionar, modificar ou excluir a fonte de dados. A DLL de instalação do driver pode solicitar que o usuário para obter informações adicionais.  
  
-   **Adicionar, modificar ou excluir fontes de dados silenciosamente.** As chamadas do programa de administração **SQLConfigDataSource** na DLL do instalador e passa-la uma janela nula manipular, o nome de uma fonte de dados para adicionar, modificar ou excluir e uma lista de valores para o registro. As chamadas DLL do instalador **ConfigDSN** na configuração do driver DLL, na verdade, adicionar, modificar ou excluir a fonte de dados.  
  
-   **Adicionar, modificar ou excluir uma fonte de dados padrão.** A fonte de dados padrão é o mesmo que qualquer outra fonte de dados, exceto que seu nome é o padrão. Ele é adicionado, modificado ou excluído da mesma forma como qualquer outra fonte de dados.
