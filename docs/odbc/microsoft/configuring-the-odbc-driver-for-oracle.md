---
title: Configurando o driver ODBC para Oracle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- configuring ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], configuring
ms.assetid: 0a5f827c-0b80-4627-85cb-f10292b9fb33
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc163f53c9dc234702f6f74426eb65f57cec26b5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096683"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>Configurar o driver ODBC para Oracle
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Você pode controlar o desempenho do driver ODBC para Oracle sabendo o ambiente de dados e definindo corretamente os parâmetros da conexão da fonte de dados por meio da caixa de diálogo [administrador de fonte de dados ODBC](../../odbc/admin/odbc-data-source-administrator.md) ou por meio de parâmetros de cadeia de conexão. A caixa de diálogo fornece os seguintes controles para se conectar a uma fonte de dados usando a caixa de diálogo ou usando cadeias de conexão:  
  
-   **Guia DSN de usuário** Lista os nomes de fonte de dados que são locais para o computador.  
  
-   **Guia DSN do sistema** Permite adicionar ou remover uma fonte de dados do sistema. As fontes de dados do sistema podem ser acessadas por todos os usuários no computador local.  
  
-   **Guia DSN de arquivo** Permite adicionar ou remover uma fonte de dados de arquivo do computador local. As fontes de dados de arquivo podem ser compartilhadas por todos os usuários que têm o mesmo driver instalado.  
  
-   **Guia Drivers** Lista os drivers ODBC instalados.  
  
-   **Guia rastreamento** Permite que você especifique como o Gerenciador de driver ODBC rastreia chamadas para funções ODBC. Você pode configurar o rastreamento separadamente para cada aplicativo ODBC instalado.  
  
-   **Guia pooling de conexão** Permite que você selecione as opções de conexão para cada driver instalado.  
  
-   **Guia sobre** Lista os arquivos de componentes ODBC instalados.  
  
 Depois de adicionar uma fonte de dados, você pode usar a caixa de diálogo **administrador de fonte de dados ODBC** para configurar o acesso à fonte de dados. Selecione uma fonte de dados e clique em uma das guias para editar ou examinar as informações.
