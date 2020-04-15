---
title: SQLDriverConnect (driver Visual FoxPro ODBC) | Microsoft Docs
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
ms.openlocfilehash: 5e270f8c9be42dc109adeaa49acb84f29f2b9511
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307087"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver Visual FoxPro ODBC. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: Completo  
  
 Conformidade da API ODBC: Nível 1  
  
 Conecta-se a uma fonte de dados existente, que pode ser um banco de [dados](../../odbc/microsoft/visual-foxpro-terminology.md) ou um diretório de [tabelas gratuitas](../../odbc/microsoft/visual-foxpro-terminology.md). As palavras-chave de atributo ODBC UID e PWD são ignoradas. A tabela a seguir lista as palavras-chave de atributo adicional suportadas.  
  
|Palavra-chave do atributo ODBC|Valor do atributo|  
|----------------------------|---------------------|  
|DSN||  
|UID|Ignorado pelo visual FoxPro ODBC Driver, mas não gera um erro.|  
|PWD|Ignorado pelo visual FoxPro ODBC Driver, mas não gera um erro.|  
|Driver|O nome e a localização do Driver Visual FoxPro ODBC; implementado pelo Driver Manager.|  
  
|Visual FoxPro ODBC Driver atributo palavra-chave|Valor do atributo|  
|-------------------------------------------------|---------------------|  
|Busca de fundo|"Sim" ou "Não"|  
|Agrupar|"Máquina" ou outra seqüência de colisão. Para obter uma lista de seqüências de colagem suportadas, consulte [SET COLLATE](../../odbc/microsoft/set-collate-command.md).|  
|Descrição||  
|Exclusivo|"Sim" ou "Não"|  
|SourceDB|Um caminho totalmente qualificado para um diretório contendo zero ou mais [tabelas gratuitas,](../../odbc/microsoft/visual-foxpro-terminology.md)ou o caminho absoluto e o nome do arquivo para um [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|SourceType|"DBC" ou "DBF"|  
|Versão||  
  
 Se o nome da fonte de dados não for especificado, o Gerenciador de driver solicita as informações ao usuário (dependendo da configuração do argumento *fDriverComplet)* e, em seguida, continua. Se mais informações forem necessárias, o driver Visual FoxPro ODBC exibirá a caixa de diálogo prompt.  
  
 Para obter mais informações, consulte [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) na *referência do programador ODBC*.
