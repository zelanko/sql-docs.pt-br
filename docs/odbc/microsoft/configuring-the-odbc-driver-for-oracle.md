---
title: Configurando o Driver ODBC para Oracle | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- configuring ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], configuring
ms.assetid: 0a5f827c-0b80-4627-85cb-f10292b9fb33
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 936664563f7ef6f717b17a2e5bb34be0df4aa6a9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>Configurando o Driver ODBC para Oracle
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Você pode controlar o desempenho do Driver ODBC para Oracle Conhecendo o ambiente de dados e configurar corretamente os parâmetros da conexão de fonte de dados por meio de [administrador de fonte de dados ODBC](../../odbc/admin/odbc-data-source-administrator.md) caixa de diálogo caixa ou por meio de se conectar parâmetros de cadeia de caracteres. A caixa de diálogo fornece os seguintes controles para se conectar a uma fonte de dados usando a caixa de diálogo ou usando cadeias de caracteres de conexão:  
  
-   **Guia DSN de usuário** lista os nomes de fonte de dados que são locais para o computador.  
  
-   **Guia DSN de sistema** permite que você adicionar ou remover uma fonte de dados do sistema. Fontes de dados do sistema podem ser acessados por todos os usuários no computador local.  
  
-   **Guia DSN de arquivo** permite que você adicionar ou remover uma fonte de dados de arquivo do computador local. Fontes de dados de arquivo podem ser compartilhados por todos os usuários que têm o mesmo driver instalado.  
  
-   **Guia drivers** lista de drivers ODBC instalados.  
  
-   **Guia rastreamento** permite que você especifique como o Gerenciador de Driver ODBC rastreia chamadas para funções ODBC. Você pode configurar o rastreamento separadamente para cada aplicativo de ODBC instalado.  
  
-   **Guia de Pooling de Conexão** permite que você selecione as opções de conexão para cada driver instalado.  
  
-   **Sobre a guia** lista os arquivos de componente ODBC instalados.  
  
 Depois de adicionar uma fonte de dados, você pode usar o **administrador de fonte de dados ODBC** caixa de diálogo para configurar o acesso à fonte de dados. Selecione uma fonte de dados e, em seguida, clique em uma das guias para editar ou examinar as informações.
