---
title: "Aplicativos compatíveis com os padrões e Drivers | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- standards-compliant applications and drivers [ODBC]
- ODBC drivers [ODBC], standards-compliant
- application features are standards-compliant [ODBC]
ms.assetid: a1145c4c-3094-4f3f-8cc2-e6bb1a930ab1
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c62e19d2d7c2c856b358649955a5b1540a802a12
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="standards-compliant-applications-and-drivers"></a>Drivers e aplicativos compatíveis com padrões
Um aplicativo compatível com os padrões ou o driver é aquele que está em conformidade com a especificação de CAE aberta do grupo "dados de gerenciamento: SQL nível de chamada CLI (Interface)" e ISO/IEC 9075-3:1995 Interface de nível de chamada (E) (SQL/CLI).  
  
 ODBC 3*. x* garante os seguintes recursos:  
  
-   Um aplicativo escrito para as especificações do Open Group e ISO CLI funcionará com um ODBC 3*. x* driver ou um driver compatível com os padrões quando ele é compilado com o ODBC 3*. x* arquivos de cabeçalho e vinculadas com ODBC 3*. x* bibliotecas, e quando ele obtém acesso do driver por meio de ODBC 3*. x* Gerenciador de Driver.  
  
-   Um driver criado às especificações do Open Group e ISO CLI funcionará com um ODBC 3*. x* aplicativo ou um aplicativo compatível com os padrões quando ele é compilado com o ODBC 3*. x* arquivos de cabeçalho e vinculado com o ODBC 3*. x* bibliotecas, e quando o aplicativo obtém acesso do driver por meio de ODBC 3*. x* Gerenciador de Driver.  
  
 Drivers e aplicativos compatíveis com os padrões são compilados com o sinalizador de compilação ODBC_STD.  
  
 Aplicativos compatíveis com padrões apresentam o seguinte comportamento:  
  
-   Se um aplicativo compatível com os padrões chama **SQLAllocEnv** (que pode ocorrer porque **SQLAllocEnv** é uma função válida no Open Group e ISO CLI), a chamada é mapeada para  **SQLAllocHandleStd** em tempo de compilação. Como resultado, em tempo de execução, o aplicativo chama **SQLAllocHandleStd**. Durante o processamento desta chamada, o Gerenciador de Driver define o atributo de ambiente SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3. Uma chamada para **SQLAllocHandleStd** é equivalente a uma chamada para **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_ENV e uma chamada para **SQLSetEnvAttr** definir SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3.  
  
-   Se um aplicativo compatível com os padrões chama **SQLBindParam** (que pode ocorrer porque **SQLBindParam** é uma função válida no Open Group e ISO CLI), o ODBC 3*. x* O Gerenciador de driver mapeia a chamada para a chamada equivalente no **SQLBindParameter**. (Consulte [SQLBindParam mapeamento](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) no Apêndice g: Driver diretrizes para compatibilidade com versões anteriores.)  
  
-   Para alinhar com a CLI ISO, o ODBC 3*. x* arquivos de cabeçalho contêm aliases para tipos de informações usados em chamadas para **SQLGetInfo**. Um aplicativo compatível com os padrões pode usar esses aliases em vez de ODBC 3*. x* tipos de informações. Para obter mais informações, consulte o próximo tópico, [arquivos de cabeçalho](../../../odbc/reference/develop-app/header-files.md).  
  
-   Um aplicativo compatível com os padrões deve verificar que todos os recursos que ele oferece suporte têm suporte no driver que funcione com. Definindo o atributo de instrução SQL_ATTR_CURSOR_SCROLLABLE a SQL_SCROLLABLE e definindo o atributo da instrução SQL_ATTR_CURSOR_SENSITIVITY SQL_INSENSITIVE ou SQL_SENSITIVE são recursos que estão disponíveis como recursos opcionais nos padrões de mas não são incluídos em ODBC 3*. x* Core nível e, portanto, pode não ter suporte de todos os ODBC 3*. x* drivers. Se um aplicativo compatível com padrões utiliza esses recursos, deve verificar se o driver que ele funcione com oferece suporte a eles.
