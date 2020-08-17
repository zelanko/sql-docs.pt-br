---
description: Entradas do Registro (Driver ODBC do Visual FoxPro)
title: Entradas do registro (driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- registry keys [ODBC]
- Visual FoxPro ODBC driver [ODBC], registry entries
- keys [ODBC]
- FoxPro ODBC driver [ODBC], registry entries
ms.assetid: 1a63d92d-ca3a-46ae-911f-6788292c801e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc4c5d617590e6435d99756b159c6049551d2d69
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340342"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>Entradas do Registro (Driver ODBC do Visual FoxPro)
Quando você instala o driver ODBC do Visual FoxPro, o programa de instalação atualiza o registro do sistema, na chave do registro HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCInst.ini, para adicionar uma nova chave chamada Microsoft Visual FoxPro driver. Sob essa chave, os valores descritos na tabela a seguir são adicionados.  
  
|Nome do valor|Tipo de valor|Valor|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|"YYN"|  
|Driver|REG_SZ|Caminho do sistema para o arquivo de vfpodbc.dll|  
|DriverODBCVer|REG_SZ|"2,50"|  
|FileExtns|REG_SZ|"*. dbf, \* . cdx, \* . FPT"|  
|Uso de|REG_SZ|"1"|  
|Instalação|REG_SZ|Caminho do sistema para o arquivo de vfpodbc.dll|  
|Sqllevel|REG_SZ|"0"|  
  
 O programa de instalação também adiciona a chave "arquivos do Visual FoxPro", representando o driver do Visual FoxPro padrão, à chave de HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini do sistema. Sob essa chave, o programa de instalação adiciona os valores descritos na tabela a seguir.  
  
|Nome do valor|Tipo de valor|Valor|  
|----------------|----------------|-----------|  
|Driver|REG_SZ|Caminho do sistema para o arquivo de vfpodbc.dll|  
  
 Cada vez que você adiciona uma fonte de dados ODBC do Visual FoxPro à sua configuração ODBC, uma nova chave é adicionada para esse nome de fonte de dados. Os valores da fonte de dados correspondem aos valores definidos na caixa de diálogo **configuração do ODBC do Visual FoxPro** , conforme listado na tabela a seguir.  
  
|Nome do valor (palavra-chave)|Tipo de valor|Valor|  
|----------------------------|----------------|-----------|  
|Agrupar|REG_SQ|Qualquer sequência de agrupamento com suporte|  
|Descrição|REG_SZ|Descrição do usuário da fonte de dados|  
|Driver||Caminho do sistema para o arquivo de vfpodbc.dll|  
|Exclusivo||Sim ou não|  
|BackgroundFetch||Sim ou não|  
|SourceDB|REG_SZ|Caminho para. Arquivo DBC|  
|SourceType|REG_SZ|"DBC" ou "DBF"|  
  
 Você não deve acessar essas informações diretamente; qualquer administração do registro é tratada pelo Administrador ODBC quando você adiciona, modifica ou exclui uma fonte de dados.  
  
 Você pode usar algumas dessas palavras-chave e valores como parâmetros na função da API do ODBC do [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) .
