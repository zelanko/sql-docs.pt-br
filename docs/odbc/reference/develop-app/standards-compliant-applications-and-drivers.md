---
title: Aplicativos e drivers compatíveis com padrões | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- standards-compliant applications and drivers [ODBC]
- ODBC drivers [ODBC], standards-compliant
- application features are standards-compliant [ODBC]
ms.assetid: a1145c4c-3094-4f3f-8cc2-e6bb1a930ab1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b4daf2e777b20b1b84c090757d0d84796a4cae1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299713"
---
# <a name="standards-compliant-applications-and-drivers"></a>Drivers e aplicativos em conformidade com padrões
Um aplicativo ou driver compatível com padrões é aquele que está em conformidade com a especificação CAE do Grupo Aberto "Gerenciamento de dados: Interface de Nível de Chamada SQL (CLI)" e a Interface de Nível de Chamada ISO/IEC 9075-3:1995 (E) (SQL/CLI).  
  
 O ODBC *3.x* garante as seguintes características:  
  
-   Um aplicativo escrito para as especificações do Open Group e ISO CLI funcionará com um driver ODBC *3.x* ou um driver compatível com padrões quando for compilado com os arquivos de cabeçalho ODBC *3.x* e vinculado com bibliotecas ODBC *3.x,* e quando ele ganhar acesso ao driver através do Gerenciador de Driver ODBC *3.x.*  
  
-   Um driver escrito nas especificações do Open Group e iso CLI funcionará com um aplicativo ODBC *3.x* ou um aplicativo compatível com padrões quando for compilado com os arquivos de cabeçalho ODBC *3.x* e vinculado com bibliotecas ODBC *3.x,* e quando o aplicativo obtém acesso ao driver através do Gerenciador de Driver ODBC *3.x.*  
  
 Aplicativos e drivers compatíveis com padrões são compilados com a bandeira de compilação ODBC_STD.  
  
 Os aplicativos compatíveis com padrões exibem o seguinte comportamento:  
  
-   Se um aplicativo compatível com padrões chamar **SQLAllocEnv** (o que pode ocorrer porque **o SQLAllocEnv** é uma função válida no Open Group e ISO CLI), a chamada é mapeada para **SQLAllocHandleStd** no momento da compilação. Como resultado, no tempo de execução, o aplicativo chama **SQLAllocHandleStd**. Durante o processamento desta chamada, o Driver Manager define o atributo de ambiente SQL_ATTR_ODBC_VERSION para SQL_OV_ODBC3. Uma chamada para **SQLAllocHandleStd** equivale a uma chamada para **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_ENV e uma chamada para **SQLSetEnvAttr** para definir SQL_ATTR_ODBC_VERSION para SQL_OV_ODBC3.  
  
-   Se um aplicativo compatível com padrões chamar **SQLBindParam** (o que pode ocorrer porque **o SQLBindParam** é uma função válida no Open Group e ISO CLI), o ODBC *3.x* Driver Manager mapeia a chamada para a chamada equivalente no **SQLBindParameter**. (Veja [o mapeamento sqlbindparam](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) no apêndice G: Diretrizes do driver para compatibilidade retrógrada.)  
  
-   Para se alinhar com a ISO CLI, os arquivos de cabeçalho ODBC *3.x* contêm aliases para tipos de informações usados em chamadas para **SQLGetInfo**. Um aplicativo compatível com padrões pode usar esses aliases em vez dos tipos de informações ODBC *3.x.* Para obter mais informações, consulte o próximo tópico, [Arquivos de cabeçalho](../../../odbc/reference/develop-app/header-files.md).  
  
-   Um aplicativo compatível com padrões deve verificar se todos os recursos suportados pelo driver com os quais ele trabalhará. Definir o atributo de declaração SQL_ATTR_CURSOR_SCROLLABLE para SQL_SCROLLABLE e definir o atributo de declaração SQL_ATTR_CURSOR_SENSITIVITY para SQL_INSENSITIVE ou SQL_SENSITIVE são recursos que estão disponíveis como recursos opcionais nos padrões, mas não estão incluídos no nível de Núcleo ODBC *3.x* e, portanto, podem não ser suportados por todos os drivers ODBC *3.x.* Se um aplicativo compatível com padrões usar esses recursos, ele deve verificar se o driver com o quais ele trabalhará os suporta.
