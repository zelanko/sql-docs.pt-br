---
title: Configurando o Driver ODBC para Oracle | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ae444cfb293e12bd94281957335da1d4f4a97885
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47831447"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>Configurar o driver ODBC para Oracle
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Você pode controlar o desempenho do Driver ODBC para Oracle Conhecendo o ambiente de dados e configurar corretamente os parâmetros da conexão de fonte de dados por meio de [administrador de fonte de dados ODBC](../../odbc/admin/odbc-data-source-administrator.md) caixa de diálogo caixa ou por meio de se conectar parâmetros de cadeia de caracteres. A caixa de diálogo fornece os seguintes controles para se conectar a uma fonte de dados usando a caixa de diálogo ou usando o connect cadeias de caracteres:  
  
-   **Guia DSN de usuário** lista os nomes de fonte de dados que são locais para o computador.  
  
-   **Guia DSN de sistema** permite que você adicionar ou remover uma fonte de dados do sistema. Fontes de dados do sistema podem ser acessadas por todos os usuários no computador local.  
  
-   **Guia DSN de arquivo** permite que você adicionar ou remover uma fonte de dados de arquivos do computador local. Fontes de dados de arquivo podem ser compartilhados por todos os usuários que têm o mesmo driver instalado.  
  
-   **Guia drivers** lista de drivers ODBC instalados.  
  
-   **Guia rastreamento** permite que você especifique como o Gerenciador de Driver ODBC rastreia chamadas para funções ODBC. Você pode configurar o rastreamento separadamente para cada aplicativo de ODBC instalado.  
  
-   **Guia de Pooling de Conexão** permite que você selecione as opções de conexão para cada driver instalado.  
  
-   **Sobre a guia** lista os arquivos de componente do ODBC instalados.  
  
 Depois de adicionar uma fonte de dados, você pode usar o **administrador de fonte de dados ODBC** caixa de diálogo para configurar o acesso à fonte de dados. Selecione uma fonte de dados e, em seguida, clique em uma das guias para editar ou examinar as informações.
