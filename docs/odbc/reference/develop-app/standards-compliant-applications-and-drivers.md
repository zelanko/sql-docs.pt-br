---
title: Aplicativos compatíveis com padrões e Drivers | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8937c2b9c80209975d03963acb19ab5da9c99e39
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811334"
---
# <a name="standards-compliant-applications-and-drivers"></a>Drivers e aplicativos em conformidade com padrões
Um aplicativo compatível com os padrões ou o driver é aquele que está em conformidade com Open CAE Especificação do grupo de "dados de gerenciamento: SQL nível de chamada CLI (Interface)" e o ISO/IEC 9075-3:1995 Interface de nível de chamada (E) (SQL/CLI).  
  
 3 de ODBC *. x* garante os seguintes recursos:  
  
-   Um aplicativo escrito com as especificações do Open Group e a CLI de ISO funcionará com um ODBC 3 *. x* driver ou um driver compatível com os padrões quando ele é compilado com o ODBC 3 *. x* arquivos de cabeçalho e vinculado com 3 de ODBC *. x* bibliotecas, e quando ele ganha acesso para o driver por meio de ODBC 3 *. x* Gerenciador de Driver.  
  
-   Um driver escrito com as especificações do Open Group e a CLI de ISO funcionará com um ODBC 3 *. x* aplicativo ou um aplicativo compatível com os padrões quando ele é compilado com o ODBC 3 *. x* arquivos de cabeçalho e vinculado com o ODBC 3 *. x* bibliotecas, e quando o aplicativo obtém acesso ao driver por meio de ODBC 3 *. x* Gerenciador de Driver.  
  
 Drivers e aplicativos compatíveis com os padrões são compilados com o sinalizador de compilação ODBC_STD.  
  
 Aplicativos compatíveis com padrões apresentam o seguinte comportamento:  
  
-   Se um aplicativo compatível com os padrões chama **SQLAllocEnv** (que pode ocorrer porque **SQLAllocEnv** é uma função válida no Open Group e ISO CLI), a chamada é mapeada para  **SQLAllocHandleStd** em tempo de compilação. Como resultado, em tempo de execução, o aplicativo chama **SQLAllocHandleStd**. Durante o processamento desta chamada, o Gerenciador de Driver define o atributo de ambiente SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3. Uma chamada para **SQLAllocHandleStd** é equivalente a uma chamada para **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV e uma chamada para **SQLSetEnvAttr** para definir SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3.  
  
-   Se um aplicativo compatível com os padrões chama **SQLBindParam** (que pode ocorrer porque **SQLBindParam** é uma função válida no Open Group e ISO CLI), o ODBC 3 *. x* Gerenciador de driver mapeia a chamada para a chamada equivalente no **SQLBindParameter**. (Consulte [mapeamento SQLBindParam](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) no Apêndice g: Driver diretrizes para compatibilidade com versões anteriores.)  
  
-   Para alinhar com a CLI do ISO, o ODBC 3 *. x* arquivos de cabeçalho contêm aliases para tipos de informações usados em chamadas aos **SQLGetInfo**. Um aplicativo compatível com os padrões pode usar esses aliases em vez de 3 a ODBC *. x* tipos de informações. Para obter mais informações, consulte o próximo tópico, [arquivos de cabeçalho](../../../odbc/reference/develop-app/header-files.md).  
  
-   Um aplicativo compatível com os padrões deve verificar que todos os recursos que ele oferece suporte a têm suporte no driver funcionará com o. Definindo o atributo de instrução SQL_ATTR_CURSOR_SCROLLABLE como SQL_SCROLLABLE e definindo o atributo da instrução SQL_ATTR_CURSOR_SENSITIVITY SQL_INSENSITIVE ou SQL_SENSITIVE são recursos que estão disponíveis como recursos opcionais nos padrões mas não estão incluídos no ODBC 3 *. x* Core nível e, portanto, pode não ter suporte por todos os ODBC 3 *. x* drivers. Se um aplicativo compatível com os padrões usa esses recursos, deve verificar que o driver que ele funcione com dá suporte a eles.
