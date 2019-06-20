---
title: As entradas do registro (Driver ODBC do Visual FoxPro) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: de287802693adb18e39509fdc0e7577d05984949
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63316832"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>Entradas do Registro (Driver ODBC do Visual FoxPro)
Quando você instala o Driver de ODBC do Visual FoxPro, o programa de instalação de atualizações de registro do sistema, na chave do registro HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCInst.ini, para adicionar uma nova chave chamada de Driver do Microsoft Visual FoxPro. Sob essa chave, os valores descritos na tabela a seguir são adicionados.  
  
|Nome do valor|Tipo de valor|Valor|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|"YYN"|  
|Driver|REG_SZ|Caminho do sistema para o arquivo vfpodbc|  
|DriverODBCVer|REG_SZ|"02.50"|  
|FileExtns|REG_SZ|"*.dbf,\*.cdx,\*.fpt"|  
|FileUsage|REG_SZ|"1"|  
|Configuração|REG_SZ|Caminho do sistema para o arquivo vfpodbc|  
|SQLLevel|REG_SZ|"0"|  
  
 O programa de instalação também adiciona a chave "Visual FoxPro Files", que representa o driver do Visual FoxPro padrão, a chave de HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini do seu sistema. Sob essa chave, o programa de instalação adiciona os valores descritos na tabela a seguir.  
  
|Nome do valor|Tipo de valor|Valor|  
|----------------|----------------|-----------|  
|Driver|REG_SZ|Caminho do sistema para o arquivo vfpodbc|  
  
 Cada vez que você adiciona uma fonte de dados ODBC do Visual FoxPro à sua configuração de ODBC, uma nova chave é adicionada para esse nome de fonte de dados. Os valores da fonte de dados correspondem aos valores definidos na **a instalação do Visual FoxPro ODBC** caixa de diálogo, conforme listado na tabela a seguir.  
  
|Nome do valor (palavra-chave)|Tipo de valor|Valor|  
|----------------------------|----------------|-----------|  
|Agrupar|REG_SQ|Nenhum suporte para a sequência de agrupamento|  
|Descrição|REG_SZ|Descrição do usuário da fonte de dados|  
|Driver||Caminho do sistema para o arquivo vfpodbc|  
|Exclusive||Sim ou Não|  
|BackgroundFetch||Sim ou Não|  
|SourceDB|REG_SZ|Caminho. Arquivo DBC|  
|SourceType|REG_SZ|"DBC" ou "DBF"|  
  
 Você não deve acessar essas informações diretamente; nenhuma administração do registro é tratada pelo administrador de ODBC quando você adicionar, modifica ou excluir uma fonte de dados.  
  
 Você pode usar algumas dessas palavras-chave e valores como parâmetros na [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) função ODBC API.
