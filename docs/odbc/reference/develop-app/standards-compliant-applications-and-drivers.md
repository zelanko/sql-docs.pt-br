---
description: Drivers e aplicativos em conformidade com padrões
title: Aplicativos e drivers em conformidade com os padrões | Microsoft Docs
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
ms.openlocfilehash: e6733afa5281f86d8dd425e6157832ee0680d34b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476378"
---
# <a name="standards-compliant-applications-and-drivers"></a>Drivers e aplicativos em conformidade com padrões
Um aplicativo ou driver em conformidade com os padrões é aquele que está de acordo com a especificação CAE do grupo aberto "Gerenciamento de Dados: CLI (interface de nível de chamada) do SQL," e a interface de nível de chamada (SQL/CLI) do ISO/IEC 9075-3:1995 (E).  
  
 O ODBC *3. x* garante os seguintes recursos:  
  
-   Um aplicativo gravado nas especificações do grupo aberto e da CLI ISO funcionará com um driver ODBC *3. x* ou com um driver compatível com padrões quando for compilado com os arquivos de cabeçalho ODBC *3. x* e vinculado com bibliotecas ODBC *3. x* e quando ele obtiver acesso ao driver por meio do Gerenciador de driver ODBC *3. x* .  
  
-   Um driver escrito nas especificações do grupo aberto e da CLI ISO funcionará com um aplicativo ODBC *3. x* ou com um aplicativo compatível com padrões quando for compilado com os arquivos de cabeçalho ODBC *3. x* e vinculado com bibliotecas ODBC *3. x* e quando o aplicativo obtiver acesso ao driver por meio do Gerenciador de driver ODBC *3. x* .  
  
 Os aplicativos e os drivers em conformidade com os padrões são compilados com o sinalizador de compilação ODBC_STD.  
  
 Os aplicativos em conformidade com os padrões apresentam o seguinte comportamento:  
  
-   Se um aplicativo compatível com padrões chamar **SQLAllocEnv** (o que pode ocorrer porque **SQLAllocEnv** é uma função válida no grupo Open e na CLI ISO), a chamada é mapeada para **SQLAllocHandleStd** no momento da compilação. Como resultado, em tempo de execução, o aplicativo chama **SQLAllocHandleStd**. Durante o curso do processamento dessa chamada, o Gerenciador de driver define o atributo de ambiente SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3. Uma chamada para **SQLAllocHandleStd** é equivalente a uma chamada para **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_ENV e uma chamada para **SQLSetEnvAttr** para definir SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3.  
  
-   Se um aplicativo compatível com padrões chamar **SQLBindParam** (que pode ocorrer porque **SQLBindParam** é uma função válida no Open Group e ISO CLI), o Gerenciador de driver ODBC *3. x* mapeia a chamada para a chamada equivalente em **SQLBindParameter**. (Consulte [mapeamento de SQLBindParam](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) no apêndice G: diretrizes de driver para compatibilidade com versões anteriores.)  
  
-   Para alinhar com a CLI ISO, os arquivos de cabeçalho ODBC *3. x* contêm aliases para tipos de informações usados em chamadas para **SQLGetInfo**. Um aplicativo compatível com os padrões pode usar esses aliases em vez dos tipos de informações do ODBC *3. x* . Para obter mais informações, consulte o próximo tópico, [arquivos de cabeçalho](../../../odbc/reference/develop-app/header-files.md).  
  
-   Um aplicativo em conformidade com os padrões deve verificar se há suporte para todos os recursos que ele suporta no driver com o qual ele trabalhará. Definir o atributo de instrução SQL_ATTR_CURSOR_SCROLLABLE como SQL_SCROLLABLE e definir o atributo de instrução SQL_ATTR_CURSOR_SENSITIVITY como SQL_INSENSITIVE ou SQL_SENSITIVE são recursos que estão disponíveis como recursos opcionais nos padrões, mas que não estão incluídos no nível de núcleo ODBC *3. x* e, portanto, podem não ter suporte de todos os drivers ODBC *3. x* . Se um aplicativo compatível com padrões usar esses recursos, ele deverá verificar se o driver com o qual ele funciona oferece suporte.
