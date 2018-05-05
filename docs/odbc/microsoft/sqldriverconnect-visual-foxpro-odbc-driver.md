---
title: SQLDriverConnect (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 10492c8f-3a18-4971-9db8-879e878083b9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d1aedce0d1e2888a4aada3a92cf0eb5973d489a5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do Driver ODBC do Visual FoxPro. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade de API de ODBC: Nível 1  
  
 Conecta-se a uma fonte de dados existente, que pode ser um [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md) ou um diretório de [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md). As ODBC atributo palavras-chave UID e PWD são ignoradas. A tabela a seguir lista as palavras-chave do atributo com suporte adicional.  
  
|Palavra-chave de atributo ODBC|Valor do atributo|  
|----------------------------|---------------------|  
|DSN||  
|UID|Ignorado pelo Driver ODBC para Visual FoxPro, mas não gera um erro.|  
|PWD|Ignorado pelo Driver ODBC para Visual FoxPro, mas não gera um erro.|  
|Driver|O nome e o local do Visual FoxPro ODBC Driver; implementado pelo Gerenciador de Driver.|  
  
|Palavra-chave atributo do Visual FoxPro ODBC Driver|Valor do atributo|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"Sim" ou "Não"|  
|Agrupar|"Computador" ou outra sequência de agrupamento. Para obter uma lista de sequências de agrupamento com suporte, consulte [definir COLLATE](../../odbc/microsoft/set-collate-command.md).|  
|Description||  
|Exclusive|"Sim" ou "Não"|  
|SourceDB|Um caminho totalmente qualificado para um diretório que contém zero ou mais [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md), ou o nome de arquivo e caminho absoluto para uma [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|SourceType|"DBC" ou "DBF"|  
|Versão||  
  
 Se o nome da fonte de dados não for especificado, o Gerenciador de Driver solicitará ao usuário para obter as informações (dependendo da configuração do *fDriverCompletion* argumento) e, em seguida, continua. Se mais informações são necessárias, o Driver de ODBC do Visual FoxPro exibe a caixa de diálogo de aviso.  
  
 Para obter mais informações, consulte [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) no *referência do programador de ODBC*.
