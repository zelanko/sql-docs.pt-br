---
title: SQLDriverConnect (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 10492c8f-3a18-4971-9db8-879e878083b9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc0bcf6a191f67b87b422b17778f56feda1f5227
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792714"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas de Driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade com a API ODBC: 1 de nível  
  
 Conecta-se a uma fonte de dados existente, que pode ser um [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md) ou um diretório de [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md). As ODBC atributo palavras-chave UID e PWD são ignoradas. A tabela a seguir lista as palavras-chave do atributo com suporte adicional.  
  
|Palavra-chave de atributo ODBC|Valor do atributo|  
|----------------------------|---------------------|  
|DSN||  
|UID|Ignorado pelo Driver de ODBC do Visual FoxPro, mas não gera um erro.|  
|PWD|Ignorado pelo Driver de ODBC do Visual FoxPro, mas não gera um erro.|  
|Driver|O nome e local do Visual FoxPro ODBC Driver; implementado pelo Gerenciador de Driver.|  
  
|Palavra-chave atributo do Visual FoxPro ODBC Driver|Valor do atributo|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"Sim" ou "Não"|  
|Agrupar|"Computador" ou outra sequência de agrupamento. Para obter uma lista de sequências de agrupamento com suporte, consulte [definir COLLATE](../../odbc/microsoft/set-collate-command.md).|  
|Description||  
|Exclusive|"Sim" ou "Não"|  
|SourceDB|Um caminho totalmente qualificado para um diretório que contém zero ou mais [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md), ou o nome de arquivo e caminho absoluto para um [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|SourceType|"DBC" ou "DBF"|  
|Versão||  
  
 Se o nome da fonte de dados não for especificado, o Gerenciador de Driver solicita ao usuário para obter as informações (dependendo da configuração do *fDriverCompletion* argumento) e, em seguida, continua. Se mais informações são necessárias, o Driver de ODBC do Visual FoxPro exibe a caixa de diálogo de aviso.  
  
 Para obter mais informações, consulte [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) na *referência do programador de ODBC*.
