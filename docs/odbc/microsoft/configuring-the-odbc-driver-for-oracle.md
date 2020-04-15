---
title: Configuração do Driver ODBC para Oracle | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1bbdbe36ed9e6f254e2b738479698bd9eece09f8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281366"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>Configurar o driver ODBC para Oracle
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Você pode controlar o desempenho do Driver ODBC para Oracle conhecendo o ambiente de dados e definindo corretamente os parâmetros da conexão de origem de dados através da caixa de diálogo [Administrador de Origem de Dados ODBC](../../odbc/admin/odbc-data-source-administrator.md) ou através de parâmetros de seqüência de string de conexão. A caixa de diálogo fornece os seguintes controles para se conectar a uma fonte de dados usando a caixa de diálogo ou usando strings de conexão:  
  
-   **Guia DSN do usuário** Lista os nomes de origem de dados que são locais para o computador.  
  
-   **Guia DSN do sistema** Permite adicionar ou remover uma fonte de dados do sistema. As fontes de dados do sistema podem ser acessadas por todos os usuários no computador local.  
  
-   **Guia DSN de arquivo** Permite adicionar ou remover uma fonte de dados de arquivo do computador local. As fontes de dados do arquivo podem ser compartilhadas por todos os usuários que têm o mesmo driver instalado.  
  
-   **Guia drivers** Lista os drivers ODBC instalados.  
  
-   **Guia de rastreamento** Permite especificar como o Gerenciador de Driver oDBC rastreia chamadas para funções ODBC. Você pode configurar o rastreamento separadamente para cada aplicativo ODBC instalado.  
  
-   **Guia de pooling de conexão** Permite selecionar opções de conexão para cada driver instalado.  
  
-   **Sobre tab** Lista os arquivos de componentes ODBC instalados.  
  
 Depois de adicionar uma fonte de dados, você pode usar a caixa de diálogo **Administrador de Origem de Dados ODBC** para configurar o acesso à sua fonte de dados. Selecione uma fonte de dados e clique em uma das guias para editar ou revisar as informações.
