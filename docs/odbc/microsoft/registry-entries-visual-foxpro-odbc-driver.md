---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 00a24ffca764c029b87470b7aa07d15f33b4c673
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67996443"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>Entradas do Registro (Driver ODBC do Visual FoxPro)
Quando você instala o driver ODBC do Visual FoxPro, o programa de instalação atualiza o registro do sistema, na chave do registro HKEY_LOCAL_MACHINE \SOFTWARE\ODBC\ODBCInst.ini, para adicionar uma nova chave chamada Microsoft Visual FoxPro driver. Sob essa chave, os valores descritos na tabela a seguir são adicionados.  
  
|Nome do valor|Tipo de valor|Valor|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|"YYN"|  
|Driver|REG_SZ|Caminho do sistema para o arquivo vfpodbc. dll|  
|DriverODBCVer|REG_SZ|"2,50"|  
|FileExtns|REG_SZ|"*. dbf,\*. cdx,\*. FPT"|  
|Uso de|REG_SZ|"1"|  
|Instalação|REG_SZ|Caminho do sistema para o arquivo vfpodbc. dll|  
|Sqllevel|REG_SZ|"0"|  
  
 O programa de instalação também adiciona a chave "arquivos do Visual FoxPro", representando o driver do Visual FoxPro padrão, à chave de \SOFTWARE\ODBC\Odbc.ini de HKEY_CURRENT_USER do seu sistema. Sob essa chave, o programa de instalação adiciona os valores descritos na tabela a seguir.  
  
|Nome do valor|Tipo de valor|Valor|  
|----------------|----------------|-----------|  
|Driver|REG_SZ|Caminho do sistema para o arquivo vfpodbc. dll|  
  
 Cada vez que você adiciona uma fonte de dados ODBC do Visual FoxPro à sua configuração ODBC, uma nova chave é adicionada para esse nome de fonte de dados. Os valores da fonte de dados correspondem aos valores definidos na caixa de diálogo **configuração do ODBC do Visual FoxPro** , conforme listado na tabela a seguir.  
  
|Nome do valor (palavra-chave)|Tipo de valor|Valor|  
|----------------------------|----------------|-----------|  
|Agrupar|REG_SQ|Qualquer sequência de agrupamento com suporte|  
|DESCRIÇÃO|REG_SZ|Descrição do usuário da fonte de dados|  
|Driver||Caminho do sistema para o arquivo vfpodbc. dll|  
|Exclusivo||Sim ou não|  
|BackgroundFetch||Sim ou não|  
|SourceDB|REG_SZ|Caminho para. Arquivo DBC|  
|SourceType|REG_SZ|"DBC" ou "DBF"|  
  
 Você não deve acessar essas informações diretamente; qualquer administração do registro é tratada pelo Administrador ODBC quando você adiciona, modifica ou exclui uma fonte de dados.  
  
 Você pode usar algumas dessas palavras-chave e valores como parâmetros na função da API do ODBC do [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) .
