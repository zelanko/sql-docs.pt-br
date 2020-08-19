---
description: SQLDriverConnect (Driver ODBC do Visual FoxPro)
title: SQLDriverConnect (driver ODBC do Visual FoxPro) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc985a5a56f54b1af8f9153bcd5129523233e2eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421790"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível 1  
  
 Conecta-se a uma fonte de dados existente, que pode ser um [banco](../../odbc/microsoft/visual-foxpro-terminology.md) de dado ou um diretório de [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md). As palavras-chave UID e PWD do atributo ODBC são ignoradas. A tabela a seguir lista as palavras-chave de atributo adicionais com suporte.  
  
|Palavra-chave de atributo ODBC|Valor do atributo|  
|----------------------------|---------------------|  
|DSN||  
|UID|Ignorado pelo driver ODBC do Visual FoxPro, mas não gera um erro.|  
|PWD|Ignorado pelo driver ODBC do Visual FoxPro, mas não gera um erro.|  
|Driver|O nome e o local do driver ODBC do Visual FoxPro; implementado pelo Gerenciador de driver.|  
  
|Palavra-chave de atributo do driver ODBC do Visual FoxPro|Valor do atributo|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"Sim" ou "não"|  
|Agrupar|"Machine" ou outra sequência de agrupamento. Para obter uma lista de sequências de agrupamento com suporte, consulte [set COLLATE](../../odbc/microsoft/set-collate-command.md).|  
|Descrição||  
|Exclusivo|"Sim" ou "não"|  
|SourceDB|Um caminho totalmente qualificado para um diretório que contém zero ou mais [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md), ou o caminho absoluto e o nome do arquivo para um [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|SourceType|"DBC" ou "DBF"|  
|Versão||  
  
 Se o nome da fonte de dados não for especificado, o Gerenciador de driver solicitará as informações ao usuário (dependendo da configuração do argumento *fDriverCompletion* ) e continuará. Se mais informações forem necessárias, o driver ODBC do Visual FoxPro exibirá a caixa de diálogo de prompt.  
  
 Para obter mais informações, consulte [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) na *referência do programador de ODBC*.
